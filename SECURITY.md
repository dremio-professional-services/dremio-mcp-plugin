# Security Policy

## Supported Versions

Only the latest released version receives security fixes.

## Reporting a Vulnerability

Report vulnerabilities privately through GitHub Security Advisories for this repository. Do not open a public issue for secrets, authentication bypasses, or sensitive endpoint exposure.

## Secret Handling

Never commit:

- Dremio PATs or API tokens
- Customer endpoints or project IDs
- Generated Dremio config files
- Local MCP client config files containing credentials

Use environment variables or local secret stores outside the repository.
