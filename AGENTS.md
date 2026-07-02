# AGENTS.md

Development guidance for agents working in this repository.

## Working Style

- Keep changes small, explicit, and scoped to the user request.
- Read the relevant existing Markdown files before changing behavior or documentation.
- Do not duplicate repository content here. Product behavior, installation, configuration, and architecture belong in `README.md` and `docs/`.
- Do not add new scripts, tests, Makefiles, CI, package managers, or extra tooling unless the user explicitly asks for them.

## Public Repository Safety

- Treat this as a public repository.
- Never commit PATs, `.env` files, customer endpoints, generated local config, or project-specific secrets.
- Keep examples generic and redact secrets in command output.

## Documentation Discipline

- Keep `README.md` current when install, usage, or repository layout changes.
- Keep the relevant files in `docs/` current when setup, configuration, architecture, or platform support changes.
- If the companion skill behavior changes, update `plugins/dremio-mcp/skills/dremio-mcp/SKILL.md`.
- If the architecture diagram changes, update both the `.drawio` source and exported `.png`.

## Versioning And Changelog

- This repository uses Semantic Versioning.
- For release-worthy changes, update all version locations together:
  - `VERSION`
  - `.claude-plugin/marketplace.json`
  - `plugins/dremio-mcp/.codex-plugin/plugin.json`
  - `plugins/dremio-mcp/.claude-plugin/plugin.json`
- Keep `CHANGELOG.md` current for every version bump.
- Use patch bumps for documentation-only changes and minor bumps for behavior, compatibility, or runtime configuration changes.

## Validation

- Run checks that match the changed files before claiming work is complete.
- For plugin changes, run the plugin validator.
- For skill changes, run the skill validator.
- For Draw.io changes, validate the `.drawio` file and inspect the exported image.
- For manifest changes, validate JSON.
- Always run `git diff --check` before committing.

## Git Discipline

- Do not commit or push unless the user explicitly asks.
- Check `git status --short` before staging.
- Stage only files that belong to the requested change.
- Never revert user changes unless explicitly requested.
- Keep commit messages terse and scoped to the actual change.
