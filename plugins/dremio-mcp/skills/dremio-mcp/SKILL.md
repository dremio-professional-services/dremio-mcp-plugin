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
3. Codex and Claude Code do not read `.env` files. Variables must be in the environment that started the agent; a `.env` file works only after `set -a; source .env; set +a` in that shell. Changes need a new agent session.
4. On Windows, restart Codex or Claude Code after changing user-level environment variables so the process inherits them.

## Defaults

The plugin sets only `PYTHONWARNINGS=ignore` and no `DREMIOAI_*` defaults. Upstream defaults apply unless the user sets them:

```text
DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF        recommended: FOR_SELF,FOR_DATA_PATTERNS
                                            add DYNAMIC_REMOTE_TOOLS for server-side AI tools
DREMIOAI_DREMIO__ENABLE_SEARCH=false        recommended: true
DREMIOAI_DREMIO__ALLOW_DML=false            read-only unless the user sets true
```

Treat `ALLOW_DML=true` as write-capable. It can allow the MCP server to create Dremio views when supported by upstream tools and user permissions.

## Tools

Read one reference, only when the task needs it:

| Need | Reference |
|---|---|
| Local tools of the MCP server, their parameters, required settings, and usage notes | [references/tools.md](references/tools.md) |
| Server-side AI tools of Dremio Cloud (SQL validation, explain, functions, engines, job profiles, wikis, labels) and how to enable them | [references/dremio-cloud-ai-tools.md](references/dremio-cloud-ai-tools.md) |

Core tools in every setup: `RunSqlQuery`, `GetSchemaOfTable`, `GetDescriptionOfTableOrSchema`, `GetTableOrViewLineage`, `GetUsefulSystemTableNames`. `SearchTableAndViews` needs `ENABLE_SEARCH=true`; `BuildUsageReport` needs a Dremio Cloud project ID. The server-side AI tools need `DYNAMIC_REMOTE_TOOLS` in `SERVER_MODE`.

For platform SQL syntax, load `dremio-cloud-sql` or `dremio-enterprise-sql`; this skill covers the MCP server only.

## Usage Rules

- Never commit PATs, project-specific endpoints, or generated Dremio config files.
- Prefer environment variables supplied by the user/session over editing plugin files.
- Before using write-capable tools, state that `ALLOW_DML=true` is active and ask for confirmation when the action may create or modify Dremio objects.
- If the MCP server fails to start or connects to an unexpected target, first check missing env vars, `uvx`, Python version, the Dremio URI, a `.env` in the server's working directory, and `~/.config/dremioai/config.yaml`; those fallbacks fill only settings missing from the environment.
