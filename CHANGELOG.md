# Changelog

All notable changes to this project are documented here.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-07-01

### Changed

- Replaced the POSIX shell-based MCP command with a cross-platform direct `uvx` command.
- Moved default MCP environment values into `.mcp.json` so macOS and Windows use the same configuration.

### Added

- Added macOS and Windows installation documentation.
- Added architecture documentation and a draw.io diagram showing one local MCP server process per agent session.
- Added configuration documentation for process environment, `.env`, and `config.yaml` precedence.

## [0.1.0] - 2026-07-01

### Added

- Initial `dremio-mcp` single-plugin marketplace for Codex and Claude Code.
- `dremio-mcp` MCP configuration derived from the validated marketplace entry for the official `dremio/dremio-mcp` server.
- Companion `dremio-mcp` skill for setup, validation, and safe usage guidance.
- Changelog, security policy, contribution guide, and Apache-2.0 license.
