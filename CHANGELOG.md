# Changelog

All notable changes to this project are documented here.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.4.0] - 2026-11-16

### Changed

- **Breaking:** Removed the `DREMIOAI_TOOLS__SERVER_MODE`, `DREMIOAI_DREMIO__ENABLE_SEARCH`, and `DREMIOAI_DREMIO__ALLOW_DML` defaults from `.mcp.json`. Plugin-set values overrode the user's environment and `.env`, so read-only mode could not be enabled. Upstream defaults now apply (`FOR_SELF`, search off, DML off) unless the user sets the variables.
- Rewrote `docs/config.md` as the single configuration reference: how variables reach the server, that Codex and Claude Code do not read `.env`, a variable table with upstream and recommended values, precedence, `.env` loading recipes, and troubleshooting.
- Replaced the Draw.io architecture diagram with Mermaid diagrams in `docs/architecture.md` and `docs/config.md`.
- Aligned `SECURITY.md` with the Dremio responsible disclosure process: private reports to security@dremio.com, expected report contents, and an extended secret-handling list.
- Restored the unmodified Apache License 2.0 text in `LICENSE`.
- Updated `AGENTS.md` to point to `CONTRIBUTING.md` and `SECURITY.md` instead of duplicating their content.

### Added

- `.env` templates for Dremio Cloud (`examples/dremio-cloud.env`) and self-managed Dremio Software (`examples/dremio-software.env`).

### Removed

- `docs/dremio-mcp-architecture.drawio` and `docs/dremio-mcp-architecture.png`.

## [0.3.0] - 2026-08-10

### Added

- Added independent SQL reference skills for current Dremio Cloud and Dremio Enterprise 26.x.
- Added topic-scoped references derived exclusively from public Dremio documentation for progressive context loading.

### Changed

- Updated plugin metadata and repository documentation for the expanded skill set.

## [0.2.1] - 2026-07-02

### Changed

- Updated the architecture diagram to show separate local MCP server processes targeting different remote Dremio instances.
- Clarified that each agent session can inherit different Dremio connection settings.

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
