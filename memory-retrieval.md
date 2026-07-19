---
id: memory-retrieval
title: Memory & Retrieval Convention
version: 1.0.0
status: active
---

# Memory & Retrieval Convention

> How KayaEOS manages context, knowledge, and information retrieval to minimize token costs while maximizing AI output quality.

## Core Principle: Load-on-Demand

KayaEOS never loads the entire framework into context. Instead, it uses a **load-on-demand** convention:

1. **Context Index** (always loaded, ~500 tokens): The minimal set of pointers AI needs to navigate the framework
2. **Retrieve on Trigger** (~2K-5K tokens each): Specific playbooks, agent definitions, or standards loaded only when needed
3. **Reference Chain** (variable): Supporting documents loaded only if referenced

## The Context Index

The context index is the entry point. It is the only file that is always loaded. Everything else is loaded on demand.

```yaml
# Conceptual structure of the context index
kaya-eos:
  constitution: constitution.md
  playbooks:
    - id: build-feature
      path: playbooks/build-feature.md
      trigger: "new feature, feature implementation, build feature"
    - id: bug-fix
      path: playbooks/bug-fix.md
      trigger: "bug, fix, debugging, issue"
    # ... all other playbooks
  agents:
    - id: architect
      path: agents/architect.md
      trigger: "architecture, design, system design"
    # ... all other agents
  adr:
    index: adr/INDEX.md
    trigger: "decision, architecture decision, ADR"
```

## Retrieval Triggers

Each playbook, agent definition, and resource has **trigger keywords**. When a developer's request matches a trigger keyword, the corresponding resource is loaded into context.

### Trigger Categories

| Category      | Triggers                                      | Example Resources  |
| ------------- | --------------------------------------------- | ------------------ |
| Feature work  | `feature`, `implement`, `build`, `develop`    | build-feature.md   |
| Bug fixing    | `bug`, `fix`, `debug`, `issue`, `error`       | bug-fix.md         |
| Refactoring   | `refactor`, `clean up`, `improve structure`   | refactor.md        |
| Code review   | `review`, `PR`, `pull request`, `code review` | code-review.md     |
| Testing       | `test`, `spec`, `coverage`, `unit test`       | testing.md         |
| Design/UI     | `design`, `UI`, `UX`, `component`, `style`    | ui-design.md       |
| Architecture  | `architecture`, `system design`, `decision`   | adr-creation.md    |
| Security      | `security`, `vulnerability`, `auth`, `CVE`    | security-review.md |
| Deployment    | `deploy`, `release`, `ship`, `production`     | deployment.md      |
| Documentation | `document`, `docs`, `readme`, `comments`      | docs.md            |

## File-Based Memory

KayaEOS uses the filesystem as its memory. There is no vector database or RAG pipeline. Instead:

### ADR as Long-Term Memory

Architecture Decision Records capture WHY decisions were made. They persist beyond any single session.

```
adr/
├── INDEX.md         # Quick lookup by keyword
├── 0001-...md       # Decision recorded
└── 0002-...md
```

### Session Context (CLAUDE.md / AGENTS.md)

The adapter-generated instruction file serves as session-level memory:

- Project conventions
- Active technology stack
- Current project phase
- Key constraints

### Playbooks as Procedural Memory

Playbooks encode HOW to perform specific tasks. They are the "muscle memory" of the framework.

## Retrieval Workflow

```
User Request
    │
    ▼
Parse trigger keywords
    │
    ▼
┌──────────────────────────────────┐
│ Load: Context Index (always)     │  ~500 tokens
│ Load: Matching Playbook(s)       │  ~2K-5K tokens each
│ Load: Matching Agent definition  │  ~500 tokens each
│ Load: Referenced ADRs (if any)   │  ~1K-2K tokens each
│ Load: Design tokens (if UI)      │  ~300 tokens
└──────────────────────────────────┘
    │
    ▼
Execute Playbook workflow
    │
    ▼
Optionally: Create ADR for decisions made
```

## Token Budget Guidelines

For any single AI interaction:

| Context Type                 | Max Tokens | Notes                            |
| ---------------------------- | ---------- | -------------------------------- |
| Context Index                | 500        | Always included                  |
| Active Playbook              | 5,000      | The playbook being executed      |
| Agent Definition             | 1,000      | The active agent(s)              |
| Supporting References        | 3,000      | ADRs, design tokens, conventions |
| **Total Framework Overhead** | **~6,000** | Before user code                 |

This leaves ample room for the actual codebase and conversation history.

## Adding New Resources

When adding a new playbook, agent, or resource:

1. Create the resource file
2. Add entry to the context index with trigger keywords
3. Ensure triggers don't collide with existing triggers
4. Update the adapter layer to include the new resource path

## AI Adapter Implementation

When generating `CLAUDE.md` or `AGENTS.md`, the adapter includes:

1. **Inline context index**: The minimal set of pointers (~500 tokens)
2. **Load instructions**: How to reference playbooks (e.g., `@playbooks/build-feature.md`)
3. **Active conventions**: Project-specific overrides

The adapter does NOT inline all playbook content. It provides the INDEX, and the AI tool retrieves full playbooks when triggered.

## Example: Feature Development Session

```
User: "Build a user login feature"

Parse triggers: feature, build, login → build-feature.md + security-review.md

Context loaded:
  ✅ Context Index (500 tokens)
  ✅ Playbook: build-feature.md (3K tokens)
  ✅ Playbook: security-review.md (2K tokens)
  ✅ Agent: implementer.md (500 tokens)
  ✅ ADR-0003 (auth pattern decision, 1K tokens)

Total framework overhead: ~7K tokens
```

This is compared to ~40K+ tokens if the entire framework were loaded.

---

_The Memory & Retrieval convention ensures KayaEOS remains token-efficient while providing comprehensive guidance when and where needed._
