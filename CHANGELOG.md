# Changelog

All notable changes to this project are documented here.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.7.0] - 2026-11-19

### Added

- `dremio-mcp` skill references: `references/tools.md` (local MCP tools, parameters, required settings, usage notes) and `references/dremio-cloud-ai-tools.md` (server-side AI tools of Dremio Cloud and how to reach them with `DYNAMIC_REMOTE_TOOLS`). `SKILL.md` routes to them.

### Fixed

- Corrected the 0.5.0 statement that server-side AI tools are exposed by default. Over stdio, which this plugin uses, they are reachable only with `DYNAMIC_REMOTE_TOOLS` in `DREMIOAI_TOOLS__SERVER_MODE`; `DREMIOAI_DREMIO__ENABLE_REMOTE_TOOLS` affects only the streamable-HTTP transport and is no longer forwarded or documented.

## [0.6.0] - 2026-11-19

### Fixed

- The MCP server no longer crashes on startup with `TypeError: Option() got an unexpected keyword argument 'click_type'`. Upstream `dremio-mcp` passes `click_type` to `typer.Option()`, which typer 0.29.0 removed, and its `typer` dependency has no upper bound. The launch command now adds `--with "typer<0.29"` until upstream is fixed.

## [0.5.0] - 2026-11-16

### Added

- `DREMIOAI_DREMIO__ENABLE_REMOTE_TOOLS` in the forwarded MCP environment and the configuration docs. Upstream `dremio-mcp` now exposes Dremio's server-side AI tools by default, independent of `DREMIOAI_TOOLS__SERVER_MODE`.
- Dremio Cloud SQL skill: recursive CTEs (`WITH RECURSIVE`), `GRANT`/`REVOKE ... ON ALL SPACES` and `ON ALL FOLDERS IN SPACE`, and `SHOW TBLPROPERTIES` with `table_property_source`.

### Changed

- Dremio Cloud SQL skill: `INSERT ... SELECT` maps columns by position; `CORR` no longer needs quoting; `CEILING`/`FLOOR` return `DECIMAL(p - s + 1, 0)` for decimal input; `CLUSTER BY` and `LOCALSORT BY` reject complex-type columns; the edition note for clustering and policies reflects the current, inconsistent public pages.
- Dremio Enterprise SQL skill: `CLUSTER BY` and `LOCALSORT BY` reject complex-type columns; `OPTIMIZE TABLE` on Open Catalog tables requires `SELECT` and `WRITE`.

### Removed

- Dremio Cloud SQL skill: the `E()` function, which is no longer documented.

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
