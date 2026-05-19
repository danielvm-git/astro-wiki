---
title: "ACPS Workflow Summary"
category: "Summaries"
---

# ACPS Workflow Summary

## Overview
ACPS Workflow (Agentic Continuous Process Selection) is a Spec Kit extension that layers delivery processes on top of Spec Kit's core spec/plan/tasks/implement loop. It adds epic backlog cycling, release planning, quality gates, and scope management.

## Core Components
- **Spec Kit Foundation**: Reuses Spec Kit's core loop (spec → plan → tasks → implement)
- **ACPS Extensions**: 
  - Epic backlog cycling (BACKLOG.md)
  - Baseline release planning
  - Plan bridging
  - Quality gates (test → UAT → docs)
  - Optional scope review
  - Release packaging
  - Change-request handling
  - BCP/FP/SNAP scope counting

## Installation Methods
1. GitHub Release (recommended): `specify extension add acps --from <release-zip>`
2. GitHub source (latest main): `specify extension add acps --from <main-zip>`
3. Local development: `specify extension add --dev /path/to/acps-workflow`

## Key Commands (speckit.acps.*)
- `speckit.acps.setup`: Bootstrap project environment, agent context, and status files
- `speckit.acps.create-epic-backlog`: Build ordered epic backlog (BACKLOG.md)
- Additional commands for release planning, quality gates, scope review, etc.

## Configuration
- Copy `config/acps-config.template.yml` to `acps-config.yml` in project
- Rely on defaults if preferred
- Troubleshooting for SSL certificate issues on macOS provided

## Integration with Hermes Agent
- Provides structured delivery process for agentic workflows
- Combines with Spec Kit for clear, agent-readable specifications
- Enables continuous process selection and improvement
- Supports epic backlog management and release planning
- Quality gates ensure thorough testing, UAT, and documentation