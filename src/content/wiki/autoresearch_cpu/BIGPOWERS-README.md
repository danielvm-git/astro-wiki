---
title: "Bigpowers Autoresearch Optimizer"
category: "Autoresearch CPU"
---

# Bigpowers Autoresearch Optimizer

This extends the autoresearch framework to optimize Bigpowers agent skills.
Instead of training neural network weights, it tunes **skill configurations**
to maximize the **BEQS** (Bigpowers Efficiency & Quality Score).

## What Was Built

### 1. SABR — Standardized Agent Benchmark Repo (`~/Developer/SABR/`)

Three benchmark tasks for measuring agent performance:

| Task | Dir | Description | Type |
|------|-----|-------------|------|
| A | `SABR/A/` | Leaky Proxy — socket leak in Node.js http-proxy | Bug Fix |
| B | `SABR/B/` | Soft-Delete — add soft-delete to Express/Prisma API | Feature |
| C | `SABR/C/` | God-Script — refactor 300-line bash spaghetti | Refactoring |

Each task has a **baseline** (broken/unfinished state) in `baseline/`. Run `reset_lab.sh` to restore.

### 2. The Orchestrator (`autoresearch_cpu/train_bigpowers.py`)

Replaces the GPT-training loop with an **agent-workflow optimizer**:

```
for each iteration:
  1. Generate random genome (skill parameters)
  2. Copy ~/Developer/skills → ~/Developer/skills-experimental
  3. Mutate SKILL.md files based on genome
  4. Reset SABR to baseline
  5. Run `hermes chat -q "<task prompt>"` against SABR task
  6. Parse output for tokens, errors, ask_user count
  7. Compute BEQS score
  8. Log result — if new best, save genome
```

**Parameters being optimized** (the "genome"):

| Parameter | Range | What It Controls |
|-----------|-------|------------------|
| `survey_detail` | 0-2 | How deep survey-context scans the codebase |
| `plan_detail` | 0-2 | How detailed plan-work output is |
| `use_grill_me` | 0/1 | Whether to stress-test plans |
| `use_request_review` | 0/1 | Whether to request code review |
| `develop_method` | 0/1 | Direct implementation vs TDD |
| `delegate_count` | 1-4 | Parallel subagents in dispatch-agents |
| `grill_rounds` | 1-3 | Rounds of grilling in grill-me |
| `use_dispatch_agents` | 0/1 | Use parallel dispatch vs sequential |

### 3. BEQS Metric

```
BEQS = (SR × QS × (1 - CC/100)) / (log10(Tokens + 1) × (A + 1))

SR  = Success Rate (0 or 1)  — all verify: commands pass?
QS  = Quality Score (0-100)   — from automated code quality checks
CC  = Compliance Violations   — % of CONVENTIONS.md violations
Tok = Total tokens consumed   — penalized logarithmically
A   = AskUserCount            — penalty for needing human help
```

## Running Experiments

```bash
# Quick test (1 iteration)
cd ~/Developer/hermes-agent/wiki/autoresearch_cpu
python3 train_bigpowers.py --task B --iterations 1

# Full run (20 iterations)  
python3 train_bigpowers.py --task A --iterations 20

# Resume interrupted run
python3 train_bigpowers.py --task B --iterations 10 --resume

# View results
column -t runs/results_B.tsv
```

## Prerequisites

- Hermes CLI installed at `~/.local/bin/hermes`
- Bigpowers skills at `~/Developer/skills/`
- Node.js installed (for SABR Tasks A and B)
- The config already points to experimental skills dir:
  `hermes config set skills.external_dirs`

## Interpreting Results

Each row in `runs/results_{task}.tsv`:

```
iter  seed  genome_hex  beqs  success  quality  violations  tokens_total  ask_user  wall_time  mutations  error
```

The `best_genome_{task}.json` file contains the best-scoring parameter
combination. Apply it to the real skills directory to lock in the improvement.

## Architecture

```
SABR/                              ← Benchmark repo (reset each iteration)
├── A/  server.js, target.js, ...  ← Leaky Proxy (NEEDS FIX)
├── B/  server.js, prisma/...      ← Soft-Delete (NEEDS FEATURE)
├── C/  backup.sh                  ← God-Script (NEEDS REFACTOR)
├── baseline/                      ← Snapshot of broken state
└── reset_lab.sh                   ← Restore broken state

skills/                            ← YOUR PRIMARY skills (read-only)
skills-experimental/               ← Mutated copies (auto-generated)

autoresearch_cpu/
├── train_cpu.py                   ← Original GPT training (unused)
├── train_bigpowers.py             ← NEW: Bigpowers optimizer
└── runs/                          ← Results
    ├── results_A.tsv
    ├── results_B.tsv
    ├── results_C.tsv
    └── best_genome_{task}.json
```
