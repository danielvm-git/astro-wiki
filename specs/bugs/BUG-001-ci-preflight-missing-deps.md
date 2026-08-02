---
bug_id: BUG-001
status: resolved
severity: high
scope: ci
title: CI Preflight step fails with 'sh: 1: astro: not found' due to dependency install order
---

# BUG-001: CI Preflight step fails with 'sh: 1: astro: not found'

## Symptom
In GitHub Actions run `30755741646`, the `test` job failed at the `Preflight` step with exit code 127 (`sh: 1: astro: not found`).

## Root Cause Analysis
In `.github/workflows/test-build-release.yml`, the `Preflight` step ran `npm run typecheck --if-present` (which executes `astro check`) BEFORE the `Install dependencies` (`npm ci`) step executed. Because `node_modules` was not yet installed, the `astro` binary could not be found in PATH.

## Fix Strategy
1. Move `Install dependencies` (`npm ci`) to run immediately after `actions/setup-node@v4` in `test-build-release.yml`.
2. Add a explicit `"preflight": "npm run typecheck"` script in `package.json` so preflight is explicitly defined.
3. Verify YAML syntax and test workflow locally.

## Verification
- Re-run local build/typecheck.
- Commit fix with `fix(ci): run npm ci before preflight step in test job`.
- Push to main and verify GitHub Actions run `Test Build Release` passes.
