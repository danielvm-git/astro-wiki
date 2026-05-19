---
title: "Autoresearch Summary"
category: "Summaries"
---

# Autoresearch Summary

## Overview
Autoresearch is a framework by Andrej Karpathy for autonomous AI research where agents iteratively improve machine learning models through self-modification and experimentation.

## Core Components
1. **prepare.py** - Fixed constants, data preparation, BPE tokenizer training, runtime utilities (not modified by agent)
2. **train.py** - Single file edited by agent containing GPT model, optimizer (Muon + AdamW), training loop (architecture, hyperparameters, optimizer, batch size all editable)
3. **program.md** - Baseline instructions for agent (edited by human to set up research organization)

## Key Mechanics
- Fixed 5-minute time budget per training run (wall clock, excluding startup/compilation)
- Metric: val_bpb (validation bits per byte) - lower is better, vocab-size independent
- Agent modifies train.py, tests for 5 minutes, keeps or discards changes based on improvement
- Human iterates on program.md to improve the research organization "code"

## Workflow
1. Agent reads program.md for context
2. Agent edits train.py to try improvements
3. Agent runs train.py for 5-minute fixed duration
4. Agent evaluates val_bpb metric
5. If improvement: keep changes; if not: discard changes
6. Repeat overnight
7. Human reviews log.md and updates program.md based on findings

## Quick Start
- Requirements: Single NVIDIA GPU (H100 tested), Python 3.10+, uv
- Install uv: `curl -LsSf https://astral.sh/uv/install.sh | sh`
- Install deps: `uv sync`
- Prepare data: `uv run prepare.py` (~2 min)
- Manual run: `uv run train.py` (~5 min)
- Autonomous mode: Point agent at program.md and instruct to kick off experiments

## Integration with Hermes Agent
- Use as engine for iterative training and process improvement
- program.md serves as lightweight "skill" for agent behavior
- Can be adapted for non-ML research by changing evaluation metric and training process