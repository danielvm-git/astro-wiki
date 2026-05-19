---
title: "Spec Kit Summary"
category: "Summaries"
---

# Spec Kit Summary

## Overview
Spec Kit is an open source toolkit that enables Spec-Driven Development (SDD), a methodology where specifications become executable and directly generate working implementations. It includes the Specify CLI, templates, scripts, and workflows to guide development teams through a structured approach.

## Core Philosophy
- Specifications are executable, not just documentation
- Focus on product scenarios and predictable outcomes
- Reduces "vibe coding" by providing structured starting points
- Supports multiple AI coding agent integrations

## Development Phases
Spec Kit outlines phases that help teams move from idea to implementation:
1. **Discovery**: Understanding the problem and defining success metrics
2. **Specification**: Creating clear, executable specifications
3. **Planning**: Breaking down specifications into actionable tasks
4. **Implementation**: Building the solution with AI agent assistance
5. **Validation**: Testing and verifying the implementation
6. **Release**: Packaging and deploying the software

## Key Components
- **Specify CLI**: Command-line interface to bootstrap projects with Spec Kit framework
- **Templates**: Pre-built structures for specs, plans, tasks, and implementation
- **Workflows**: Guided processes for each development phase
- **AI Agent Integrations**: Support for various AI coding assistants (Claude, Codex, Gemini, etc.)
- **Extensions & Presets**: Community-contributed additions to customize the toolkit

## Integration Architecture
Spec Kit uses a plugin system for AI agents:
- Each agent is a self-contained integration subpackage under `src/specify_cli/integrations/<key>/`
- Integrations inherit from base classes (MarkdownIntegration, TomlIntegration, YamlIntegration, SkillsIntegration, or IntegrationBase)
- The Integration Registry (`INTEGRATION_REGISTRY`) tracks all available agents
- Context files (like AGENTS.md) provide instructions to agents within the Spec Kit framework

## Adding a New Integration
1. Choose appropriate base class based on agent's needs
2. Create subpackage with required fields: `key`, `config`, `registrar_config`, `context_file`
3. Register the integration in `src/specify_cli/integrations/__init__.py`
4. Set up context file behavior (usually handled automatically)
5. Test integration with `specify init` and `specify integration uninstall`

## Supported AI Coding Agents
Spec Kit includes built-in integrations for:
- Claude (SkillsIntegration)
- Gemini CLI (TomlIntegration)
- Windsurf (MarkdownIntegration)
- GitHub Copilot (IntegrationBase)
- And others via community extensions

## Quick Start
1. Install Specify CLI (requires uv)
2. Bootstrap a project: `specify init my-project --integration <key>`
3. Follow the guided workflow to create specs, plans, and tasks
4. Use AI agent to implement based on the specifications

## Integration with Hermes Agent
- Provides structured Spec-Driven Development workflow
- Offers clear, agent-readable specifications
- Supports multiple AI agent integrations for flexibility
- Enables executable specifications that generate working implementations
- Includes quality gates and validation processes
- Complements ACPS Workflow and BMAD Method for comprehensive agentic development