---
id: adr-0001
title: Use KayaEOS as the foundational development framework
status: accepted
date: 2026-07-19
deciders:
  - Cüneyt Kaya
supersedes:
  - none
superseded_by:
  - none
---

# ADR-0001: Use KayaEOS as the Foundational Development Framework

## Context

AI-assisted software development tools (Claude Code, GitHub Copilot, Cursor, Codex, etc.) are rapidly evolving. Each tool has its own instruction format, context conventions, and prompt patterns. Without a unified framework:

- Instructions must be duplicated across tools
- Engineering standards are inconsistently applied
- Switching AI tools requires rewriting prompts
- There is no single source of truth for development workflow

## Decision

Adopt KayaEOS (Kaya Engineering OS) as the foundational meta-framework for all AI-assisted software development.

KayaEOS provides:

1. **Engineering Constitution** — Immutable principles that precede any specific tool
2. **Playbook Library** — Standard workflows for all development scenarios
3. **Agent Catalog** — Specialist agent definitions
4. **AI Adapter Layer** — Single canonical source → multiple tool outputs
5. **ADR System** — Decision tracking
6. **Memory & Retrieval** — Context management convention

All future project infrastructure (CI/CD, linting, testing, design systems) will be structured according to KayaEOS conventions.

## Options Considered

### Option 1: Per-Tool Prompts (Status Quo)

Maintain separate prompt files for Claude, Copilot, Cursor, etc.

- **Pros**: Simple, no abstraction overhead
- **Cons**: Duplication, inconsistency, high maintenance as tools evolve, no single source of truth
- **Why rejected**: Violates the DRY principle at the meta level; unsustainable as the AI tool ecosystem grows

### Option 2: Single Monolithic Master Prompt

One massive prompt file containing all rules, workflows, and conventions.

- **Pros**: Single file, easy to version
- **Cons**: Token-expensive on every use, hard to maintain, tool-specific formatting, no modular loading
- **Why rejected**: High token costs, poor maintainability, contradicts the modular philosophy

### Option 3: KayaEOS Meta-Framework (Selected)

A modular, tool-agnostic framework with a single canonical source and adapter-generated tool outputs.

- **Pros**: Model-agnostic, modular (load-on-demand), single source of truth, versionable, diffable, human-readable
- **Cons**: Initial setup overhead, requires discipline to maintain
- **Why selected**: Only option that meets all requirements: tool independence, token efficiency, maintainability, and scalability

## Consequences

### Positive

- Engineering standards survive any individual AI tool change
- Playbooks are reusable across projects
- Token costs are minimized through load-on-demand
- ADR system provides institutional memory
- All tool instruction files generated from canonical source

### Negative

- Initial effort to create and maintain the framework
- Requires team discipline to follow the system
- Need to update adapters when new AI tools emerge

### Neutral / Side Effects

- Framework itself becomes a living project requiring maintenance
- May influence future tooling choices toward KayaEOS-compatible tools

## References

- [KayaEOS Constitution](../constitution.md)
- [brainstorming notes](../brainstorming)
- [KayaEOS Repository Blueprint](../blueprint.md)

---

_This ADR was created following the KayaEOS ADR system._
