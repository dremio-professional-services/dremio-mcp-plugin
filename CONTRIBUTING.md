# Contributing

## Development

Keep this repository small. It should contain the marketplace metadata, plugin manifests, `.mcp.json`, the `dremio-mcp` configuration skill, the independent `dremio-cloud-sql` and `dremio-enterprise-sql` skills, and standard repository documentation. Maintain the SQL skills as public-documentation-only and platform-isolated; do not introduce shared SQL references or Cloud/Enterprise availability assumptions.

## Versioning

Use Semantic Versioning:

- Patch: documentation fixes or MCP config metadata fixes without behavior changes.
- Minor: new plugin capabilities, new skill guidance, or compatible MCP configuration changes.
- Major: breaking changes to env vars, MCP server names, marketplace names, or install flow.

When changing the version, update:

- `VERSION`
- `CHANGELOG.md`
- `.claude-plugin/marketplace.json`
- `plugins/dremio-mcp/.codex-plugin/plugin.json`
- `plugins/dremio-mcp/.claude-plugin/plugin.json`

When changing runtime behavior, update `docs/installation.md` and `docs/architecture.md` if the user-facing setup or process model changes.

## Pull Requests

Keep changes scoped. Do not add wrapper scripts, tests, generated config files, or credentials unless the repository direction changes explicitly.
