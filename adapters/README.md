---
id: adapter-layer
title: AI Adapter Layer Specification
version: 1.0.0
status: active
---

# AI Adapter Layer

> The adapter layer is the bridge between KayaEOS canonical sources and AI tool-specific instruction files.

## Architecture

```
KayaEOS Canonical Sources (Single Source of Truth)
    │
    ├── constitution.md         # Engineering Constitution
    ├── blueprint.md            # Repository Blueprint
    ├── memory-retrieval.md     # Memory & Retrieval Convention
    ├── playbooks/              # All playbooks
    ├── agents/                 # All agent definitions
    ├── adr/                    # Architecture Decision Records
    │
    ▼
Context Index (context-index.yml)
    │
    ▼
┌─────────────────────────────────────┐
│        Adapter Layer (Generator)    │
│                                     │
│  Reads canonical sources            │
│  Reads context index                │
│  Generates tool-specific outputs    │
└─────────────────────────────────────┘
    │
    ├── ▶ CLAUDE.md              # Claude Code instructions
    ├── ▶ AGENTS.md              # AGENTS.md standard
    ├── ▶ copilot-instructions/  # GitHub Copilot
    │       .github/copilot-instructions.md
    ├── ▶ .cursorrules           # Cursor IDE
    └── ▶ .windsurfrules         # Windsurf IDE
```

## How It Works

1. **Canonical Sources** are the single source of truth. All content lives here.
2. **Context Index** (`context-index.yml`) maps trigger keywords to canonical resources. This is the load-on-demand index.
3. **Tool-Specific Outputs** are generated from the canonical sources using the context index. Each output is tailored to the specific tool's conventions.

## What Each Output Contains

### CLAUDE.md (Claude Code)

Claude Code uses `CLAUDE.md` for project-level instructions. The adapter generates:

- A minimal inlined context index (~500 tokens)
- Core constitution principles (abbreviated)
- Load instructions: how to reference playbooks using `@` syntax
- Project-specific overrides (if any)

### AGENTS.md

AGENTS.md is an emerging standard for agent-compatible projects. The adapter generates:

- A minimal inlined context index (~500 tokens)
- Agent catalog summary
- Playbook reference table with triggers
- Load-on-demand instructions

### GitHub Copilot Instructions

`.github/copilot-instructions.md` — The adapter generates:

- Coding conventions
- Design token rules
- Testing requirements
- Accessibility standards

## Context Index Format

The context index is a YAML file that maps triggers to resources:

```yaml
version: "1.0"
resources:
  - type: playbook
    id: build-feature
    path: playbooks/build-feature.md
    triggers: ["feature", "implement", "build", "develop"]
    tokens: ~3500
  - type: agent
    id: architect
    path: agents/architect.md
    triggers: ["architecture", "system design", "ADR"]
    tokens: ~800
```

## Token Budget

Each generated output must stay within these limits:

| Section              | Max Tokens        |
| -------------------- | ----------------- |
| Inline context index | 500               |
| Core principles      | 300               |
| Playbook/agent table | 300               |
| Load instructions    | 200               |
| **Total per output** | **~1,300 tokens** |

This ensures the adapter output is cheap to include in every session, while the full playbook content is loaded on demand.

## Generation

To regenerate adapter outputs after changes to canonical sources:

1. Update the canonical source (playbook, constitution, agent, etc.)
2. Update `context-index.yml` if triggers or paths changed
3. Regenerate tool-specific outputs using the canonical sources
4. Commit both the canonical changes AND the regenerated outputs

## Adding a New AI Tool

To add support for a new AI tool:

1. Create a new output template in `adapters/`
2. Map the canonical fields to the tool's expected format
3. Add the file path to the generation list
4. Regenerate all outputs

Never hand-edit generated files. Always update the canonical source and regenerate.
