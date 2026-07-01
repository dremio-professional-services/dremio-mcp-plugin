---
name: dremio-mcp
description: Use when Codex needs to configure, validate, or use the Dremio MCP local server for Dremio Cloud or self-managed Dremio clusters; trigger for dremio-mcp MCP setup, DREMIOAI_DREMIO__URI/PAT/project configuration, Dremio catalog inspection, SQL execution through MCP tools, or troubleshooting Dremio MCP access.
---

# Dremio MCP

Use the `dremio-mcp` MCP server from this plugin when an agent needs live Dremio catalog, schema, workload, or SQL-query access.

## Setup Checks

1. Confirm `uvx` is available: `uvx --version`.
2. Confirm the runtime environment has:
   - `DREMIOAI_DREMIO__URI`: `prod`, `prodemea`, or a full Dremio coordinator/API URL.
   - `DREMIOAI_DREMIO__PAT`: personal access token or compatible secret.
   - `DREMIOAI_DREMIO__PROJECT_ID`: required for Dremio Cloud projects.
3. If read-only access is required, set `DREMIOAI_DREMIO__ALLOW_DML=false` before starting the agent.
4. On Windows, restart Codex or Claude Code after changing user-level environment variables so the process inherits them.

## Defaults

The MCP config sets these cross-platform defaults:

```text
DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF,FOR_DATA_PATTERNS
DREMIOAI_DREMIO__ENABLE_SEARCH=true
DREMIOAI_DREMIO__ALLOW_DML=true
PYTHONWARNINGS=ignore
```

Treat `ALLOW_DML=true` as write-capable. It can allow the MCP server to create Dremio views when supported by upstream tools and user permissions.

## Usage Rules

- Never commit PATs, project-specific endpoints, or generated Dremio config files.
- Prefer environment variables supplied by the user/session over editing plugin files.
- Before using write-capable tools, state that `ALLOW_DML=true` is active and ask for confirmation when the action may create or modify Dremio objects.
- If the MCP server fails to start or connects to an unexpected target, first check missing env vars, `uvx`, Python version, the Dremio URI, a project-local `.env`, and `~/.config/dremioai/config.yaml`.
