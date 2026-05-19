---
title: "The Agentic Coding Stack"
category: "Pages"
---

# The Agentic Coding Stack

This framework, as described in the DevGenius blog, defines the necessary components for reliable and efficient autonomous AI coding.

## The 5 Layers

1.  **Delivery Methodology:** Defines the sequence of analysis, planning, and implementation (e.g., `BMAD-METHOD`, `spec-kit`).
2.  **Agent Discipline:** Governs the AI's behavior during execution, enforcing habits like TDD and systematic debugging (e.g., `superpowers`).
3.  **Technical Context:** Provides semantic understanding of the codebase, such as blast radius and logic slices (e.g., `Ctxo`).
4.  **Token Optimization:** Manages the context window by filtering noisy shell output or sandboxing tool execution (e.g., `RTK`, `context-mode`).
5.  **Product Surface:** Offers an integrated operating environment for autonomous work, tracking state and milestones (e.g., `gsd-2`).

## The 7 Essential Tools

*   **BMAD-METHOD:** A heavy, opinionated methodology with 34+ workflows for structured multi-phase delivery.
*   **spec-kit:** A lighter, spec-driven toolkit for standardizing requirements across different AI platforms.
*   **superpowers:** A skill library that injects engineering discipline (TDD, verification gates) into agent behavior.
*   **Ctxo:** An MCP server for deep semantic analysis, answering complex questions about code relationships and impact.
*   **RTK:** A Rust-based CLI proxy that filters and compresses shell command output to save tokens.
*   **context-mode:** An MCP server that sandboxes execution, allowing agents to analyze data internally and return only relevant results.
*   **gsd-2:** A full autonomous platform that coordinates planning, execution, and verification in a controlled environment.

---
**Source:** [The Agentic Coding Stack – Blog.DevGenius.io](https://blog.devgenius.io/the-agentic-coding-stack-7-tools-5-layers-and-the-missing-link-nobody-has-built-yet-de264b260db3)
