# CONVENTIONS.md — astro-wiki Governance

## Conventional Commits & SemVer
All commits must strictly follow Conventional Commits 1.0.0 (`type(scope): description`).

## Git Attribution Policy
NEVER include `Co-authored-by`, `Co-Authored-By`, or any AI agent attribution footer in git commits. All commits appear as authored by human user.

## CI/CD & Security Architecture
- Workflows must reside in `.github/workflows/` adhering to `danielvm-git/.github` v4.1.0 guidelines.
- Workflows must pin third-party actions, define explicit `permissions:`, use Node 22, and employ `npm` dependency caching.
- Production bundles are built once in CI, passing `deploy-meta.json` artifact to CD.
- Deployments require post-deploy health checks against live site URLs.
