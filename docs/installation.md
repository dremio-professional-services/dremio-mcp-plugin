# Installation

This guide installs the `dremio-mcp` plugin and configures the local Dremio MCP server. Installing the plugin registers the MCP server definition and makes its three skills available.

The plugin starts one local MCP server process through `uvx` per Codex or Claude Code session, so `uvx` and Python are plugin runtime prerequisites. The two SQL reference skills' bundled content and answers remain offline: they do not depend on MCP connectivity, a PAT, an endpoint, environment configuration, or a live Dremio connection. Secrets stay outside the repository and are read from the environment that starts the agent.

Connection settings, `.env` handling, and precedence are described in [config.md](config.md). This page only covers installation.

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

Set the Dremio connection variables in your shell profile as described in [config.md](config.md#shell-profile-recommended), then open a new terminal.

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

Set the Dremio connection variables as user environment variables as described in [config.md](config.md#shell-profile-recommended), then open a new terminal. Windows processes do not see user-level environment changes until they restart.

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

## Troubleshooting

- `uvx` not found: install `uv`, open a new terminal, and make sure `uvx` is in `PATH`.
- Plugin not visible: restart the agent session after install or update.
- Connection problems: see [config.md](config.md#troubleshooting).
