# shirman-digest — Claude Code Plugin

## Release Workflow

After ANY version bump, feature, or fix:

1. **CHANGELOG.md** (English) — add entry with `Added`/`Fixed`/`Improved` prefix
2. **CHANGELOG.ru.md** (Russian) — add matching entry translated to Russian
3. **Both files must stay in sync** — same versions, same entries, same order
4. Bump version in `plugins/shirman-digest/.claude-plugin/plugin.json` AND `.claude-plugin/marketplace.json`
5. Copy updated SKILL.md to root: `cp plugins/shirman-digest/skills/shirman-digest/SKILL.md ./SKILL.md`
6. Commit, push to `main`

## Changelog Format

Follow [Claude Code style](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md):
- `## X.Y.Z` headings, newest first
- Bullet list with action words: Added, Fixed, Improved, Changed, Removed
- No dates (version = identifier)

## Language

- SKILL.md, CHANGELOG.ru.md — Russian
- CHANGELOG.md, README.md, plugin.json — English
- Commit messages — Russian
