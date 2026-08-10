# Installation

This guide installs the `dremio-mcp` plugin and configures the local Dremio MCP server. Installing the plugin registers the MCP server definition and makes its three skills available.

The plugin starts one local MCP server process through `uvx` per Codex or Claude Code session, so `uvx` and Python are plugin runtime prerequisites. The two SQL reference skills' bundled content and answers remain offline: they do not depend on MCP connectivity, a PAT, an endpoint, environment configuration, or a live Dremio connection. Secrets stay outside the repository and are read from the launching process environment.

For MCP connection-setting precedence between process environment variables, `.env`, and `~/.config/dremioai/config.yaml`, see [config.md](config.md).

## Plugin Installation And Runtime Prerequisites

- Git
- `uvx` from `uv`
- Python 3.11 or newer available to `uv`
- Codex CLI when installing for Codex
- Claude Code CLI when installing for Claude Code

## MCP Connection Prerequisites

- A Dremio PAT
- A Dremio endpoint:
  - Dremio Cloud shortcut such as `prod` or `prodemea`
  - Self-managed URL such as `https://dremio.example.com:443`

## macOS

Install `uv` for the plugin runtime with Homebrew:

```bash
brew install uv
```

Alternative standalone installer:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Open a new terminal and verify:

```bash
uv --version
uvx --version
```

Verify the agent CLI you want to use:

```bash
codex --version
claude --version
```

If `uv` cannot find a suitable Python runtime:

```bash
uv python install 3.11
```

To use the MCP server against Dremio, set environment variables in the shell that starts Codex or Claude Code:

```bash
export DREMIOAI_DREMIO__URI=prodemea
export DREMIOAI_DREMIO__PAT="$(cat ~/.dremio/token)"
export DREMIOAI_DREMIO__PROJECT_ID="<project-id>"
```

Optional read-only mode:

```bash
export DREMIOAI_DREMIO__ALLOW_DML=false
```

Install for Codex:

```bash
codex plugin marketplace add dremio-professional-services/dremio-mcp-plugin --ref main
codex plugin add dremio-mcp@dremio-mcp-plugin
```

Install for Claude Code:

```bash
claude plugin marketplace add dremio-professional-services/dremio-mcp-plugin
claude plugin install dremio-mcp@dremio-mcp-plugin
```

Start a new Codex or Claude Code session after installation.

## Windows

Install `uv` for the plugin runtime with WinGet:

```powershell
winget install --id=astral-sh.uv -e
```

Alternative with Scoop:

```powershell
scoop install main/uv
```

Alternative standalone installer:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Open a new PowerShell window and verify:

```powershell
uv --version
uvx --version
```

Verify the agent CLI you want to use:

```powershell
codex --version
claude --version
```

If `uv` cannot find a suitable Python runtime:

```powershell
uv python install 3.11
```

To use the MCP server against Dremio, set user-level environment variables:

```powershell
[Environment]::SetEnvironmentVariable("DREMIOAI_DREMIO__URI", "prodemea", "User")
[Environment]::SetEnvironmentVariable("DREMIOAI_DREMIO__PAT", "<pat>", "User")
[Environment]::SetEnvironmentVariable("DREMIOAI_DREMIO__PROJECT_ID", "<project-id>", "User")
```

Optional read-only mode:

```powershell
[Environment]::SetEnvironmentVariable("DREMIOAI_DREMIO__ALLOW_DML", "false", "User")
```

Open a new terminal after setting variables. Windows processes do not reliably see user-level environment changes until they restart.

Install for Codex:

```powershell
codex plugin marketplace add dremio-professional-services/dremio-mcp-plugin --ref main
codex plugin add dremio-mcp@dremio-mcp-plugin
```

Install for Claude Code:

```powershell
claude plugin marketplace add dremio-professional-services/dremio-mcp-plugin
claude plugin install dremio-mcp@dremio-mcp-plugin
```

Start a new Codex or Claude Code session after installation.

## MCP Runtime Defaults

The plugin sets these defaults in `.mcp.json`:

```text
DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF,FOR_DATA_PATTERNS
DREMIOAI_DREMIO__ENABLE_SEARCH=true
DREMIOAI_DREMIO__ALLOW_DML=true
PYTHONWARNINGS=ignore
```

Override them in the launching environment when needed. Set `DREMIOAI_DREMIO__ALLOW_DML=false` for read-only use.

The upstream Dremio MCP server can also read `.env` from the process current working directory and `~/.config/dremioai/config.yaml` as a fallback. See [config.md](config.md) before relying on those files for shared setup.

## Troubleshooting

- `uvx` not found: install `uv`, open a new terminal, and make sure `uvx` is in `PATH`.
- Missing Dremio credentials: set `DREMIOAI_DREMIO__URI` and `DREMIOAI_DREMIO__PAT` in the environment that launches Codex or Claude Code.
- Dremio Cloud project not found: set `DREMIOAI_DREMIO__PROJECT_ID`.
- Unexpected Dremio target: check for a project-local `.env` and for an existing `~/.config/dremioai/config.yaml`.
- Plugin not visible: restart the agent session after install or update.
