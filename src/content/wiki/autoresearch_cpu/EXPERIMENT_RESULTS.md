---
title: "Bigpowers Autoresearch — Experiment Results & Improvements"
category: "Autoresearch CPU"
---

# Bigpowers Autoresearch — Experiment Results & Improvements

## Experiment Summary

Ran 3 SABR tasks (A, B, C) across 4 methodologies (bigpowers, spec-kit, bmad, acps).

### Task A: Leaky Proxy (Bug Fix)
| Methodology | Status | Wall Time | Result |
|---|---|---|---|
| bigpowers | ✅ Pass | 101s | All 5 bug fixes applied |
| spec-kit | ❌ Fail | - | Agent API 400 error |
| bmad | ❌ Fail | - | Agent API 400 error |
| acps | ❌ Fail | - | Agent API 400 error |

### Task B: Soft-Delete (Feature)
| Methodology | Status | Wall Time | Tests | Specs |
|---|---|---|---|---|
| bigpowers | ✅ Pass | 409s | 7/7 | 5 |
| spec-kit | ✅ Pass | 283s | 15/15 | 1 |
| bmad | ✅ Pass | 122s | 10/10 | 0 |
| acps | ✅ Pass | 237s | 10/10 | 0 |

### Task C: God-Script (Refactoring)
| Methodology | Status | Wall Time | Tests | Notes |
|---|---|---|---|---|
| bigpowers | ✅ Pass | manual | 12/12 | All functions < 20 lines, single upload function |
| spec-kit | ⏸️ Pending | - | - | Not run (API errors) |
| bmad | ⏸️ Pending | - | - | Not run (API errors) |
| acps | ⏸️ Pending | - | - | Not run (API errors) |

## Key Findings

### 1. Environment Setup is the #1 Blocker
- Prisma 7.x requires adapter-based config vs Prisma 5.x simple URL format
- Without `--yolo`, agents get stuck on interactive command approval prompts
- Pre-installing dependencies reduced wall time by ~40%
- **Recommendation**: Add environment setup as a prerequisite step in program.md

### 2. Prompt Style Dramatically Affects Performance
- Tight, direct prompts ("Do X, Y, Z") outperformed workflow-follow prompts
- "Be direct and fast" reduced wall time from ~400s to ~100s for Task A
- Spec-kit's spec-first approach produced the most comprehensive tests (15 vs 7)
- **Recommendation**: Add prompt templates for each methodology

### 3. Context Length Limits Agent Effectiveness
- After ~20 tool calls, agent API started returning 400 errors
- Longer conversations = higher chance of API failure
- **Recommendation**: Use shorter, focused sessions; reset context between tasks

### 4. Reset Between Runs is Critical
- `git reset --hard HEAD` + `git clean -fd` needed but Hermes blocks git commands
- Leftover working tree changes caused subsequent runs to inherit prior implementations
- **Recommendation**: Use file-based reset (write_file to restore baselines) instead of git

### 5. Test Quality Varies by Methodology
- Spec-kit: 15 tests (most thorough, spec-driven)
- BMAD/ACPS: 10 tests each (good coverage)
- Bigpowers: 7 tests (adequate but minimal)
- **Recommendation**: Add enforce-first skill to all methodology prompts

## Bigpowers Skill Improvements

### New Skills to Add

1. **setup-environment** — Pre-install dependencies, configure tools before starting work
   - Detect project type (Node.js, Python, Bash)
   - Install required packages
   - Configure database connections
   - Verify environment is ready

2. **reset-baseline** — Restore project to known state between experiment runs
   - Write baseline files from templates
   - Remove generated artifacts
   - Verify clean state

3. **run-methodology** — Execute a specific methodology prompt template
   - Takes methodology name as parameter
   - Loads appropriate prompt template
   - Tracks wall time and results
   - Logs to results TSV

### Existing Skills to Improve

1. **develop-tdd** — Add environment setup step before TDD loop
2. **investigate-bug** — Add leak detection pattern (Task A)
3. **plan-refactor** — Add Stepdown Rule enforcement (< 20 lines/function)
4. **audit-code** — Add shellcheck compliance check for bash scripts

## Superpowers Integration

The SKILL-INDEX references "superpowers (obra)" as the base framework with 14 core skills.
Current bigpowers skills derived from superpowers:
- develop-tdd ← superpowers/tdd
- delegate-task ← superpowers/subagent-driven-development
- dispatch-agents ← superpowers/dispatching-parallel-agents
- execute-plan ← superpowers/executing-plans
- audit-code ← superpowers/requesting-code-review
- request-review ← superpowers/requesting-code-review
- respond-review ← superpowers/receiving-code-review
- commit-message ← superpowers/finishing-a-development-branch
- plan-work ← superpowers/writing-plans
- investigate-bug ← superpowers/systematic-debugging
- validate-fix ← superpowers/verification-before-completion
- kickoff-branch ← superpowers/using-git-worktrees
- seed-conventions ← superpowers/writing-skills
- craft-skill ← superpowers/writing-skills

### Additional Superpowers to Add

From the superpowers framework (https://github.com/obra/superpowers):
1. **brainstorming** — Pre-implementation ideation (already in elaborate-spec)
2. **writing-plans** — Already mapped to plan-work
3. **executing-plans** — Already mapped to execute-plan
4. **subagent-driven-development** — Already mapped to delegate-task
5. **dispatching-parallel-agents** — Already mapped to dispatch-agents
6. **requesting-code-review** — Already mapped to audit-code/request-review
7. **receiving-code-review** — Already mapped to respond-review
8. **finishing-a-development-branch** — Already mapped to commit-message/release-branch
9. **using-git-worktrees** — Already mapped to kickoff-branch
10. **systematic-debugging** — Already mapped to investigate-bug
11. **verification-before-completion** — Already mapped to validate-fix
12. **writing-skills** — Already mapped to craft-skill/seed-conventions
13. **tdd** — Already mapped to develop-tdd

### New Skills Not Yet in Bigpowers

1. **slice-tasks** — Break work into vertical slices (referenced in SKILL-INDEX but not in ~/Developer/skills/)
2. **scope-work** — Define in/out of scope (referenced in SKILL-INDEX but not in ~/Developer/skills/)
3. **challenge-design** — Stress-test design (referenced as grill-me)
4. **grill-with-docs** — Grill assumptions with real docs
5. **diagnose-root** — 4-phase root cause analysis
6. **design-interface** — API shape proposals
7. **session-state** — Track implementation decisions
8. **trace-requirement** — Link stories to implementation
9. **assess-impact** — Analyze blast radius
10. **change-request** — Add/reorder requirements
11. **release-branch** — Merge/PR decision
12. **inspect-quality** — Structured QA session
13. **terse-mode** — Ultra-compressed output
14. **edit-document** — Restructure documents
15. **visual-dashboard** — Browser-based architecture dashboard
16. **wire-observability** — Structured logging
17. **hook-commits** — Pre-commit hooks
18. **guard-git** — Block dangerous git commands
19. **organize-workspace** — Clean workspace

## Methodology Comparison Matrix

| Criteria | Bigpowers | Spec-Kit | BMAD | ACPS |
|---|---|---|---|---|
| **Best for** | Greenfield | Quality | Speed | Process |
| **Test coverage** | 7/7 (adequate) | 15/15 (best) | 10/10 (good) | 10/10 (good) |
| **Wall time** | 409s | 283s | 122s* | 237s |
| **Specs created** | 5 | 1 | 0 | 0 |
| **From scratch** | ✅ | ✅ | ❌ | ❌ |
| **Complexity** | High | Medium | Low | Medium |

*BMAD was fastest because it inherited a working implementation.

## Recommendations for Future Runs

1. **Always use `--yolo`** for non-interactive command execution
2. **Pre-install dependencies** before launching agent sessions
3. **Use tight, direct prompts** with explicit step-by-step instructions
4. **Reset baseline between runs** using file writes (not git commands)
5. **Limit context length** — start fresh sessions for each methodology
6. **Add environment setup** as a prerequisite step
7. **Use spec-kit for test-heavy tasks** — it produced the most comprehensive tests
8. **Use bigpowers for greenfield work** — it creates the most thorough artifacts
9. **Use bmad for quick iterations** — it's the fastest when implementation exists
10. **Add superpowers skills** that are missing from the current bigpowers set
