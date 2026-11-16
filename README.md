# Dremio MCP Plugin

Single-plugin marketplace for installing the local Dremio MCP configuration and three bundled skills in Codex or Claude Code. The `dremio-mcp` skill covers MCP setup; the `dremio-cloud-sql` and `dremio-enterprise-sql` skills provide independent, platform-specific SQL guidance for current Dremio Cloud and Dremio Enterprise 26.x.

The plugin exposes a cross-platform `dremio-mcp` MCP entry for the official [`dremio/dremio-mcp`](https://github.com/dremio/dremio-mcp) server. It starts the server locally through `uvx` for each Codex or Claude Code session. The SQL skills do not depend on MCP connectivity: each loads only its own topic-scoped references derived from public Dremio documentation, without a shared SQL reference core. The repository does not store Dremio endpoints, PATs, or project IDs.

## Install

See [docs/installation.md](docs/installation.md) for macOS and Windows setup. For MCP connection settings, see [docs/config.md](docs/config.md) for configuration precedence.

Plugin installation and runtime prerequisites:

- Git
- Codex CLI or Claude Code CLI
- `uvx` from the [uv package manager](https://docs.astral.sh/uv/)
- Python 3.11 or newer available to `uv`

The installed plugin registers the MCP server and starts it through `uvx` for each Codex or Claude Code session, so `uvx` and Python are runtime prerequisites. The two SQL reference skills' bundled content and answers remain offline: they do not depend on MCP connectivity, a PAT, an endpoint, environment configuration, or a live Dremio connection.

To use the local MCP server against Dremio, provide a Dremio PAT and endpoint. Dremio documents MCP setup and endpoint choices in the [Dremio MCP guide](https://docs.dremio.com/dremio-cloud/ai-integration/mcp-server/). Set the connection values in the environment that starts your agent:

```bash
export DREMIOAI_DREMIO__URI=prodemea
export DREMIOAI_DREMIO__PAT=@~/.dremio/token
export DREMIOAI_DREMIO__PROJECT_ID="<project-id>"
```

Codex and Claude Code do not read `.env` files, and the plugin sets no `DREMIOAI_*` defaults. The server runs read-only with the basic tool set unless you enable search, data-pattern tools, or DML. See [docs/config.md](docs/config.md) for all variables, `.env` usage, and precedence.

### Codex

```bash
codex plugin marketplace add dremio-professional-services/dremio-mcp-plugin --ref main
codex plugin add dremio-mcp@dremio-mcp-plugin
```

Start a new Codex session after installation so the three skills and MCP server definition are loaded.

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
docs/config.md                        connection variables, .env usage, and precedence
docs/architecture.md                  local MCP runtime architecture
examples/dremio-cloud.env             .env template for a Dremio Cloud project
examples/dremio-software.env          .env template for self-managed Dremio Software
plugins/dremio-mcp/.mcp.json          dremio-mcp MCP entry
plugins/dremio-mcp/skills/dremio-mcp/ MCP configuration skill
plugins/dremio-mcp/skills/dremio-cloud-sql/
                                        Current non-Classic Dremio Cloud SQL skill; load only for scoped SQL
                                        or metadata-query requests after platform confirmation
plugins/dremio-mcp/skills/dremio-enterprise-sql/
                                        Dremio Enterprise 26.x SQL skill; load only for scoped SQL or
                                        metadata-query requests after edition and version confirmation
```

## Versioning

This repository uses Semantic Versioning. The current version is in `VERSION`, plugin manifests, and `CHANGELOG.md`.

## Security

Do not commit PATs, private endpoints, or customer/project-specific values. Report security issues privately as described in `SECURITY.md`.
