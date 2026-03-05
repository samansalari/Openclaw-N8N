# BOOTSTRAP.md - First Run Setup

Welcome to life, N8nOps! Follow these steps to set up your connection to the n8n instance.

## Step 1: Verify n8n is Accessible

Run:
```bash
curl -s -o /dev/null -w "%{http_code}" http://localhost:5678/healthz
```

Expected: `200`. If not, the n8n instance may not be running.

## Step 2: Set Up API Key

The human needs to create an n8n API key:
1. Open http://localhost:5678 in the browser
2. Go to Settings > API
3. Create a new API key
4. Store it securely

Ask the human for the API key, then test it:
```bash
curl -s -H "X-N8N-API-KEY: THE_KEY" http://localhost:5678/api/v1/workflows | head -c 200
```

If it returns workflow data, the key works. Store it as an environment variable `N8N_API_KEY`.

## Step 3: Inventory Existing Workflows

```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/workflows | jq '.data[] | {id, name, active}'
```

Update MEMORY.md with the workflow catalog.

## Step 4: Inventory Credentials

```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" http://localhost:5678/api/v1/credentials | jq '.data[] | {id, name, type}'
```

Update MEMORY.md and TOOLS.md with the credential inventory.

## Step 5: Verify Your Skills

Read through the skill files in `skills/n8n/` to confirm your knowledge:
- `skills/n8n/SKILL.md` — capability overview
- `skills/n8n/node-catalog.md` — verified node types
- `skills/n8n/ai-patterns.md` — AI workflow patterns
- `skills/n8n/api-reference.md` — REST API reference
- `skills/n8n/templates.md` — workflow templates

## Step 6: Clean Up

Once setup is complete:
1. Update IDENTITY.md with any personality tweaks
2. Update MEMORY.md with the instance details
3. Delete this BOOTSTRAP.md file — you won't need it again

Tell the human: "N8nOps is online. Connected to n8n at localhost:5678. Ready to build, debug, and manage workflows."
