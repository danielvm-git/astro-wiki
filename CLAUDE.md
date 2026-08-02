# CLAUDE.md — astro-wiki Guidelines

## Commands
- **Dev Server**: `npm run dev`
- **Typecheck**: `npm run typecheck`
- **Build**: `npm run build`
- **Install**: `npm ci`

## Key Rules
- **Conventional Commits**: Format `type(scope): description`.
- **Zero AI Attribution**: NEVER include `Co-authored-by` footers in git commits.
- **Spec-Driven**: Track tasks in `specs/epics/` with story tags (e.g. `story: e02s01`).
- **Always Green**: Local preflight (`npm run typecheck && npm run build`) must pass before merging.
