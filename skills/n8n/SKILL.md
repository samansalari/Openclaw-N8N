# n8n Workflow Management Skill

## Overview

This skill gives you complete mastery of n8n workflow automation. You can create, edit, debug, test, deploy, and monitor n8n workflows through the REST API.

## Capabilities

### Workflow CRUD
- List all workflows (`GET /api/v1/workflows`)
- Create workflows from natural language descriptions
- Read and analyze existing workflows
- Update workflow nodes, connections, parameters
- Delete workflows (with confirmation)
- Activate/deactivate workflows

### Execution Management
- List executions with filters (status, workflow, date range)
- View execution details including node-level results
- Identify and diagnose failed executions
- Retry failed workflows
- Clean up old executions

### Credential Management
- List available credentials and their types
- Verify credential connectivity
- Guide credential setup through the browser

### Workflow Building
- Construct valid n8n workflow JSON from requirements
- Wire nodes with correct connection types (main, ai_languageModel, ai_tool, etc.)
- Set proper node parameters and typeVersions
- Handle AI/LangChain node patterns (agents, chains, RAG, memory)

### Debugging
- Trace execution failures to specific nodes
- Diagnose expression errors (`={{ }}` syntax)
- Fix connection issues (wrong type, missing connections)
- Identify hallucinated/invalid node types

### Testing
- Trigger manual workflow executions via API
- Send test payloads to webhook endpoints
- Validate workflow JSON structure before deployment
- Check for common mistakes (orphan nodes, missing respondToWebhook, etc.)

## Slash Commands

- `/n8n-status` — Check n8n instance health and overview
- `/n8n-list` — List all workflows with status
- `/n8n-create` — Create a new workflow from description
- `/n8n-debug` — Debug a failing workflow
- `/n8n-test` — Test a workflow with sample data
- `/n8n-exec` — View recent executions
- `/n8n-creds` — List credentials

## Required Tools

- `exec` — For curl commands to the n8n REST API (primary)
- `web_fetch` — For simple GET requests
- `browser` — For visual n8n UI operations (credential setup, execution viewing)

## References

See the following files in this skill folder:
- `node-catalog.md` — Complete verified node type catalog
- `ai-patterns.md` — AI/LangChain workflow patterns and connection types
- `api-reference.md` — n8n REST API endpoint reference
- `templates.md` — Ready-to-use workflow templates
