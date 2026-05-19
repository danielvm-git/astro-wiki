---
title: "Clean Code for AI Agents"
category: "Pages"
---

# Clean Code for AI Agents

Based on the principles outlined by AkitaOnRails, this guide focuses on re-evaluating traditional software engineering principles for an era where LLMs are the primary readers and editors of code.

## Key Principles

### 1. Shift in Audience
Code is no longer written primarily for humans, but for AI agents. Principles must account for technical constraints like context window limits, attention degradation, and tool-call costs.

### 2. Small Units are Mandatory
Functions and files must be kept small (ideally under 300 lines). This ensures a complete unit of logic fits within a single tool call, allowing the agent to reason with "full attention" without truncating data.

### 3. "Grepability" as an API
Agents navigate codebases using lexical search (`grep`/`ripgrep`) rather than vector databases. Use unique, highly descriptive names (e.g., `UserRegistrationValidator` instead of `Validator`) to allow agents to find targets instantly without noise.

### 4. The Return of Comments
Unlike traditional Clean Code, which views comments as "failures," AI agents thrive on them. Comments should provide **provenance and intent**—explaining *why* a specific workaround exists or referencing issue IDs—context that isn't visible in the syntax alone.

### 5. Explicit Typing & Contextual Errors
Use explicit types and provide rich context in error messages. This reduces the "hallucination" rate by giving the agent clear boundaries and actionable feedback when things fail.

### 6. Predictable Structure
Maintain a rigid, consistent directory structure and coding style. Consistency reduces the "cognitive load" (token usage) for the agent when internalizing the project's patterns.

### 7. Testability for Agents
Write tests that are easy for an agent to run and interpret. Small, focused test suites with clear output allow agents to validate their own changes autonomously and cheaply.

---
**Source:** [Clean Code pra Agentes de IA – AkitaOnRails.com](https://akitaonrails.com/2026/04/20/clean-code-para-agentes-de-ia/)
