# HEARTBEAT.md - N8nOps Periodic Checks

## n8n Health Monitoring

On each heartbeat, check the following:

### 1. n8n Instance Health
```bash
curl -s -o /dev/null -w "%{http_code}" -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/workflows
```
- If NOT 200: Alert the human immediately that n8n is down

### 2. Failed Executions (last hour)
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "http://localhost:5678/api/v1/executions?status=error&limit=5"
```
- If any errors found: Report the workflow name, error message, and timestamp
- Include a brief diagnosis if possible

### 3. Active Workflow Count
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "http://localhost:5678/api/v1/workflows?active=true" | jq '.data | length'
```
- Log the count in daily memory file

## When to Alert vs Stay Quiet

**Alert the human when:**
- n8n instance is unreachable
- Multiple workflow executions have failed
- A critical workflow (any with "prod" or "live" in the name) fails

**Stay quiet (HEARTBEAT_OK) when:**
- Everything is healthy
- No failed executions
- No changes since last check

## Memory Update

After checking, update `memory/heartbeat-state.json`:
```json
{
  "lastCheck": "ISO_TIMESTAMP",
  "n8nStatus": "healthy|down",
  "failedExecutions": 0,
  "activeWorkflows": 0
}
```
