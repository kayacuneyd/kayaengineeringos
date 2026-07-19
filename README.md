# Kaya Engineering OS (KayaEOS)

> A model-agnostic, version-controlled, modular engineering framework for AI-assisted software development.

## What is KayaEOS?

KayaEOS is a **meta-framework** designed to standardize software development processes and achieve consistent, high-quality outputs from AI tools (Claude Code, Codex, GitHub Copilot, Cursor, Windsurf, etc.).

Instead of a single monolithic prompt, it is a modular system that lives on GitHub — versioned, maintainable, and tool-agnostic.

## Why?

- AI models change; your engineering principles should endure
- **Single canonical source** instead of separate prompts per AI tool
- **Load-on-demand convention** minimizes token costs
- One reference point for all new projects

## Components

| Component                    | Description                                                            |
| ---------------------------- | ---------------------------------------------------------------------- |
| **Engineering Constitution** | Immutable engineering principles (the constitution)                    |
| **Repository Blueprint**     | Standard directory structure and file conventions                      |
| **ADR System**               | Architecture Decision Records for tracking decisions                   |
| **Playbook Library**         | Standard workflows for all development scenarios                       |
| **Agent Catalog**            | Role and responsibility definitions for specialist agents              |
| **AI Adapter Layer**         | Generate CLAUDE.md, AGENTS.md, Copilot instructions from single source |
| **Memory & Retrieval**       | Context and knowledge management convention                            |

## Usage

To use KayaEOS in your own project:

1. Browse this repo, read the Engineering Constitution
2. Copy AI Adapter outputs (CLAUDE.md or AGENTS.md) into your project
3. Reference the relevant playbook when working with your AI tool

```bash
# When developing a feature:
"@playbooks/build-feature.md follow this playbook to implement feature X"

# When reviewing code:
"@playbooks/code-review.md review this PR according to this playbook"
```

## Philosophy

- **Model-agnostic**: Processes stay the same even when AI tools change
- **Human-readable**: Markdown + YAML frontmatter, accessible everywhere
- **Git-friendly**: Every component is versionable and diffable
- **Modular**: Load only what you need, avoid unnecessary context
- **Pragmatic**: Working solutions over theoretical perfection

## Status

🚧 **v0.1.0-alpha** — Under active development. Building blocks in progress.

## License

MIT © Cüneyt Kaya
