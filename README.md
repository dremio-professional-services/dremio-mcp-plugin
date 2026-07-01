# Dremio MCP Plugin

Single-plugin marketplace for installing the Dremio cluster MCP configuration and companion skill in Codex or Claude Code.

The plugin exposes a cross-platform `dremio-mcp` MCP entry for the official [`dremio/dremio-mcp`](https://github.com/dremio/dremio-mcp) server. It starts the server locally through `uvx` for each Codex or Claude Code session. It does not store Dremio endpoints, PATs, or project IDs in the repository.

## Install

See [docs/installation.md](docs/installation.md) for macOS and Windows setup, and [docs/config.md](docs/config.md) for configuration precedence.

Prerequisites:

- `uvx` from the [uv package manager](https://docs.astral.sh/uv/)
- Git
- A Dremio PAT and endpoint. Dremio documents MCP setup and endpoint choices in the [Dremio MCP guide](https://docs.dremio.com/dremio-cloud/ai-integration/mcp-server/).

Set connection values in the environment that launches your agent:

```bash
export DREMIOAI_DREMIO__URI=prodemea
export DREMIOAI_DREMIO__PAT="$(cat ~/.dremio/token)"
export DREMIOAI_DREMIO__PROJECT_ID='replace-for-dremio-cloud'
```

Optional defaults:

```bash
export DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF,FOR_DATA_PATTERNS
export DREMIOAI_DREMIO__ENABLE_SEARCH=true
export DREMIOAI_DREMIO__ALLOW_DML=true
```

Set `DREMIOAI_DREMIO__ALLOW_DML=false` for read-only use. The inherited default is `true`, which can allow upstream MCP tools to create Dremio views when the authenticated user has permission.

### Codex

```bash
codex plugin marketplace add dremio-professional-services/dremio-mcp-plugin --ref main
codex plugin add dremio-mcp@dremio-mcp-plugin
```

Start a new Codex session after installation so the skill and MCP server are loaded.

For local development from this checkout:

```bash
codex plugin marketplace add .
codex plugin add dremio-mcp@dremio-mcp-plugin
```

### Claude Code

```bash
claude plugin marketplace add dremio-professional-services/dremio-mcp-plugin
claude plugin install dremio-mcp@dremio-mcp-plugin
```

Then run `/reload-plugins` inside Claude Code or start a fresh session. Claude Code MCP CLI syntax is documented in Anthropic's [MCP setup guide](https://code.claude.com/docs/en/mcp).

## Repository Layout

```text
.agents/plugins/marketplace.json      Codex marketplace index
.claude-plugin/marketplace.json       Claude Code marketplace index
docs/installation.md                  macOS and Windows install guide
docs/config.md                        environment, .env, and config.yaml precedence
docs/architecture.md                  local MCP runtime architecture
plugins/dremio-mcp/.mcp.json          dremio-mcp MCP entry
plugins/dremio-mcp/skills/dremio-mcp/ companion skill
```

## Versioning

This repository uses Semantic Versioning. The current version is in `VERSION`, plugin manifests, and `CHANGELOG.md`.

## Security

Do not commit PATs, private endpoints, or customer/project-specific values. Report security issues privately as described in `SECURITY.md`.
