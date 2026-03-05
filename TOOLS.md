# TOOLS.md - N8nOps Local Configuration

## n8n Instance Connection

- **n8n Base URL:** `http://localhost:5678`
- **n8n API Base:** `http://localhost:5678/api/v1`
- **n8n API Key:** (set via `N8N_API_KEY` environment variable or use the value stored in secrets)
- **n8n Version:** 2.0.0

## How to Call the n8n API

### Using exec (curl) — Primary Method

All n8n API calls use the `X-N8N-API-KEY` header for authentication.

```bash
# List all workflows
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/workflows

# Get specific workflow
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/workflows/WORKFLOW_ID

# Create workflow (POST with JSON body)
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" -H "Content-Type: application/json" \
  -d '{"name":"My Workflow","nodes":[...],"connections":{}}' \
  http://localhost:5678/api/v1/workflows

# Update workflow (PUT with full JSON body)
curl -s -X PUT -H "X-N8N-API-KEY: $N8N_API_KEY" -H "Content-Type: application/json" \
  -d '{"name":"Updated","nodes":[...],"connections":{}}' \
  http://localhost:5678/api/v1/workflows/WORKFLOW_ID

# Activate workflow
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  http://localhost:5678/api/v1/workflows/WORKFLOW_ID/activate

# Deactivate workflow
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  http://localhost:5678/api/v1/workflows/WORKFLOW_ID/deactivate

# Delete workflow
curl -s -X DELETE -H "X-N8N-API-KEY: $N8N_API_KEY" \
  http://localhost:5678/api/v1/workflows/WORKFLOW_ID

# List executions (with optional filters)
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "http://localhost:5678/api/v1/executions?workflowId=ID&status=error&limit=10"

# Get execution details
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  http://localhost:5678/api/v1/executions/EXECUTION_ID

# List credentials
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/credentials

# List tags
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/tags
```

### Using web_fetch — Alternative Method

For simpler GET requests, use web_fetch with the full URL and appropriate headers.

### Using browser — Visual Method

For operations that are easier via the n8n UI (credential setup, testing webhook triggers, viewing execution results), use the browser tool to navigate to the n8n dashboard.

- **n8n Editor:** `http://localhost:5678`
- **n8n Workflow Editor:** `http://localhost:5678/workflow/WORKFLOW_ID`
- **n8n Executions:** `http://localhost:5678/executions`

## Available Credentials in n8n

(Update this list after connecting to the instance)

- TODO: Run `curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/credentials` and populate this section

## Important Notes

- The n8n API requires an API key. Generate one from n8n Settings > API.
- Large workflow JSON should be saved to a temp file and sent via `curl -d @file.json`
- When creating/updating workflows, always send the COMPLETE nodes and connections arrays
- Workflow IDs are strings (not integers)
- Execution data can be very large — use `?limit=` to paginate
