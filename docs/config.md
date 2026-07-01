# Configuration

This plugin does not store Dremio endpoints, PATs, project IDs, or generated Dremio config files. It starts the upstream `dremio/dremio-mcp` server locally and passes configuration through the MCP server process environment.

## Plugin Defaults

The plugin defines these default process environment values in `plugins/dremio-mcp/.mcp.json`:

```text
DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF,FOR_DATA_PATTERNS
DREMIOAI_DREMIO__ENABLE_SEARCH=true
DREMIOAI_DREMIO__ALLOW_DML=true
PYTHONWARNINGS=ignore
```

Set `DREMIOAI_DREMIO__ALLOW_DML=false` in the environment that launches Codex or Claude Code when you want read-only use.

Connection-specific values must come from the user environment or another upstream Dremio MCP config source:

```text
DREMIOAI_DREMIO__URI
DREMIOAI_DREMIO__PAT
DREMIOAI_DREMIO__PROJECT_ID
```

`DREMIOAI_DREMIO__PROJECT_ID` is required for Dremio Cloud projects. For self-managed Dremio, use a full HTTPS URL such as `https://dremio.example.com:443`.

## Upstream Resolution Order

After the local process starts, the upstream Dremio MCP server resolves settings in this order:

1. Programmatic or CLI initialization values.
2. Real process environment variables such as `DREMIOAI_DREMIO__URI`.
3. A `.env` file in the process current working directory, if present.
4. The default YAML config file.
5. File secrets supported by Pydantic settings.

For normal plugin use, the important order is:

```text
process environment > .env in current working directory > default config.yaml
```

That means explicit environment variables are the safest way to make the plugin deterministic.

## Default Config File

The upstream server uses this default config path:

```text
$XDG_CONFIG_HOME/dremioai/config.yaml
```

If `XDG_CONFIG_HOME` is not set, it falls back to:

```text
~/.config/dremioai/config.yaml
```

This path is used on macOS, Linux, and Windows. On Windows with no `XDG_CONFIG_HOME`, that typically means:

```text
C:\Users\<user>\.config\dremioai\config.yaml
```

If the file already exists, the upstream server reads it. If `DREMIOAI_DREMIO__URI`, `DREMIOAI_DREMIO__PAT`, or `DREMIOAI_DREMIO__PROJECT_ID` are not set in the process environment or `.env`, values from this YAML file can be used silently.

If the file does not exist, the upstream server may create an empty config file at that path during startup.

Example YAML:

```yaml
dremio:
  uri: "prodemea"
  pat: "@~/tokens/dremio.pat"
  project_id: "00000000-0000-0000-0000-000000000000"
  enable_search: true
  allow_dml: false
tools:
  server_mode: "FOR_SELF,FOR_DATA_PATTERNS"
```

The `@` prefix for `pat` tells the upstream server to read the PAT from a local file.

## `.env` Files

The upstream server also reads `.env` from the current working directory of the Codex or Claude Code process. This matters because the plugin no longer changes into `/tmp` before running `uvx`.

That is intentional for cross-platform support, but it means a project-local `.env` can affect the MCP server.

Example `.env`:

```text
DREMIOAI_DREMIO__URI=prodemea
DREMIOAI_DREMIO__PAT=@~/tokens/dremio.pat
DREMIOAI_DREMIO__PROJECT_ID=00000000-0000-0000-0000-000000000000
DREMIOAI_DREMIO__ALLOW_DML=false
```

Do not commit `.env` files that contain PATs or customer-specific endpoints.

## Recommended Practice

- Set `DREMIOAI_DREMIO__URI`, `DREMIOAI_DREMIO__PAT`, and `DREMIOAI_DREMIO__PROJECT_ID` in the environment that launches Codex or Claude Code.
- Use `DREMIOAI_DREMIO__ALLOW_DML=false` unless write-capable Dremio MCP tools are expected.
- Keep PATs in a secret manager or token file, and pass them with the upstream `@file` syntax when useful.
- Check for a project-local `.env` when the MCP server connects to an unexpected Dremio target.
- Check `~/.config/dremioai/config.yaml` when environment variables are missing or behavior differs across machines.

## Quick Checks

macOS or Linux:

```bash
env | grep '^DREMIOAI_' | sed -E 's/(DREMIOAI_DREMIO__PAT=).*/\1<redacted>/'
test -f .env && sed -E 's/(DREMIOAI_DREMIO__PAT=).*/\1<redacted>/' .env
test -f ~/.config/dremioai/config.yaml && sed -E 's/(pat:).*/\1 "<redacted>"/' ~/.config/dremioai/config.yaml
```

Windows PowerShell:

```powershell
Get-ChildItem Env:DREMIOAI_* | ForEach-Object {
  if ($_.Name -eq "DREMIOAI_DREMIO__PAT") { "$($_.Name)=<redacted>" } else { "$($_.Name)=$($_.Value)" }
}
Test-Path .env
$cfg = Join-Path $HOME ".config\dremioai\config.yaml"
Test-Path $cfg
if (Test-Path $cfg) { Get-Content $cfg | ForEach-Object { $_ -replace '(^\s*pat:\s*).*', '$1"<redacted>"' } }
```

Avoid pasting PAT values into issues, logs, or pull requests.

## Upstream References

- [Dremio MCP settings documentation](https://github.com/dremio/dremio-mcp/blob/main/docs/settings.md)
- [Dremio MCP settings source](https://github.com/dremio/dremio-mcp/blob/main/src/dremioai/config/settings.py)
