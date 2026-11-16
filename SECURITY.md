# Security Policy

## Supported Versions

Only the latest release receives security fixes (see
[CHANGELOG.md](CHANGELOG.md)).

## Reporting a Vulnerability

Report vulnerabilities privately by email to
[security@dremio.com](mailto:security@dremio.com), Dremio's channel for
responsible disclosure. Do not open a public issue or pull request for
security problems such as leaked secrets, authentication bypasses, or
sensitive endpoint exposure.

Please include:

- a description of the vulnerability and its impact,
- the affected component (this repository, the plugin manifests,
  `.mcp.json`, or a skill) and versions (plugin, `dremio-mcp`, Dremio),
- steps to reproduce, and supporting material such as requests, responses,
  or logs, with all secrets removed.

Dremio's [responsible disclosure policy](https://www.dremio.com/platform/security/responsible-disclosure-limitations/)
applies, including its out-of-scope list. There is no bug bounty program.

## Secret Handling

Never commit:

- Dremio PATs, OAuth tokens, or passwords
- Customer endpoints, project IDs, or customer-specific configuration
- Generated Dremio config files
- Local MCP client config files containing credentials, such as
  `claude_desktop_config.json`, `config.yaml`, or `.env` files

Use environment variables or local secret stores outside the repository.
