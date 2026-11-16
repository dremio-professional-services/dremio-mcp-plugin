# AGENTS.md

Development guidance for agents working in this repository.

## Working Style

- Keep changes small, explicit, and scoped to the user request.
- Read `README.md`, `CONTRIBUTING.md`, and the relevant files in `docs/` before changing behavior or documentation. They are the single sources for usage, development rules, and architecture; link to them instead of repeating their content here or elsewhere.
- Preserve unrelated worktree changes.
- Do not add new scripts, tests, Makefiles, CI, package managers, or extra tooling unless the user explicitly asks for them.

## Public Repository Safety

- Treat this as a public repository (Apache License 2.0) and follow `SECURITY.md`.
- Never commit PATs, `.env` files, customer endpoints, generated local config, or project-specific secrets.
- Keep examples generic and redact secrets in command output.

## Documentation Discipline

- Keep `README.md` current when install, usage, or repository layout changes.
- Keep the relevant files in `docs/` current when setup, configuration, architecture, or platform support changes.
- If the companion skill behavior changes, update `plugins/dremio-mcp/skills/dremio-mcp/SKILL.md`.
- Keep diagrams as Mermaid code blocks in the Markdown files; do not add image or Draw.io diagram sources.

## Versioning And Changelog

- This repository uses Semantic Versioning.
- For release-worthy changes, update all version locations together, as listed in "Versioning" in `CONTRIBUTING.md`.
- Keep `CHANGELOG.md` current for every version bump.
- Use patch bumps for documentation-only changes and minor bumps for behavior, compatibility, or runtime configuration changes.

## Validation

- Run checks that match the changed files before claiming work is complete.
- For plugin changes, run the plugin validator.
- For skill changes, run the skill validator.
- For Mermaid changes, render the diagram (for example with `npx -y @mermaid-js/mermaid-cli`) to check that it parses.
- For manifest changes, validate JSON.
- Always run `git diff --check` before committing.

## Git Discipline

- Do not commit or push unless the user explicitly asks.
- Check `git status --short` before staging.
- Stage only files that belong to the requested change.
- Never revert user changes unless explicitly requested.
- Never force-push, amend published commits, or bypass hooks with `--no-verify` unless explicitly requested.
- Before committing, check the staged diff for secrets and run `git diff --cached --check`.
- Keep commit messages terse and scoped to the actual change.

## Review Checklist

- [ ] No local tool settings or credentials are staged.
- [ ] No secrets, customer endpoints, or local paths were added.
- [ ] Each changed fact is updated in its single source document, not copied.
- [ ] Version locations and `CHANGELOG.md` agree for release-worthy changes.
- [ ] `git diff --check` passes for unstaged and staged changes.
- [ ] Only requested files are staged.
