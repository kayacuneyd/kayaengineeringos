---
id: repo-blueprint
title: KayaEOS Repository Blueprint
version: 1.0.0
status: active
---

# Repository Blueprint

> The standard directory structure and file conventions for all KayaEOS-compliant projects.

## Standard Directory Structure

```
project-root/
├── README.md                   # Project overview, setup, usage
├── CHANGELOG.md                # Human-readable release history
├── LICENSE                     # License file
├── CONTRIBUTING.md            # Contribution guidelines
├── constitution.md             # KayaEOS constitution (can be a symlink to main repo)
│
├── design/                     # Design system
│   ├── tokens/                 # Design tokens (the single source of truth)
│   │   ├── colors.yml
│   │   ├── typography.yml
│   │   └── spacing.yml
│   ├── design-principles.md    # Project-specific design principles
│   ├── component-library.md    # Component inventory and usage rules
│   └── ui-patterns.md          # Recurring UI patterns
│
├── docs/                       # Project documentation
│   ├── architecture.md         # High-level architecture overview
│   ├── api.md                  # API documentation
│   └── guides/                 # How-to guides
│
├── adr/                        # Architecture Decision Records
│   ├── INDEX.md                # Index of all ADRs
│   ├── _template.md           # ADR template
│   ├── 0001-use-kaya-eos.md    # Example ADR
│   └── ...
│
├── src/                        # Source code (framework-specific)
│   ├── components/             # UI components
│   ├── lib/                    # Business logic / utilities
│   ├── hooks/                  # Framework hooks (if applicable)
│   ├── pages/                  # Page components (if applicable)
│   └── ...
│
├── tests/                      # Test files
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── public/                     # Static assets
│   ├── images/
│   └── fonts/
│
├── .github/                    # GitHub-specific configuration
│   ├── workflows/              # CI/CD workflows
│   └── copilot-instructions.md # GitHub Copilot instructions
│
├── .vscode/                    # Editor settings (optional, git-ignored by default)
│   └── settings.json
│
├── AI-AGENTS.md                # AGENTS.md standard (for compatible tools)
├── CLAUDE.md                   # Claude Code instructions
│
├── .gitignore
├── .editorconfig
├── .prettierrc
├── eslint.config.mjs           # or equivalent linter config
└── package.json                # or equivalent manifest
```

## File Naming Conventions

### Markdown Files

- **UPPERCASE** for top-level meta files: `README.md`, `CHANGELOG.md`, `CLAUDE.md`
- **lowercase-with-hyphens** for everything else: `build-feature.md`, `ui-patterns.md`

### Source Code

- Follow the framework/language conventions
- Components: `PascalCase` (React, Vue, Svelte)
- Utilities: `camelCase.ts` or `snake_case.py`
- Tests: match the source file name + `.test` or `_test`

### ADR Files

- Pattern: `NNNN-lowercase-with-hyphens.md`
- Example: `0001-use-kaya-eos.md`, `0002-choose-postgres-over-mongodb.md`

## Required Files for Every Project

Every KayaEOS-compliant project MUST include:

1. **README.md** — Answers "what, why, how to run, how to contribute"
2. **CHANGELOG.md** — Following [Keep a Changelog](https://keepachangelog.com/)
3. **constitution.md** — Link or copy of the KayaEOS constitution
4. **adr/INDEX.md** — Index of all ADRs
5. **design/tokens/** — At minimum: colors, typography, spacing tokens
6. **AI-AGENTS.md** or **CLAUDE.md** — AI tool instructions (generated from adapter)

## Design System Requirements

### Design Tokens (design/tokens/)

Every project must define these token categories:

**colors.yml**

```yaml
# Example structure
primary:
  50: "#EFF6FF"
  100: "#DBEAFE"
  500: "#3B82F6"
  700: "#1D4ED8"
neutral:
  50: "#F9FAFB"
  900: "#111827"
semantic:
  success: "#10B981"
  warning: "#F59E0B"
  error: "#EF4444"
```

**typography.yml**

```yaml
# Example structure
fontFamily:
  sans: "Inter, system-ui, sans-serif"
  mono: "JetBrains Mono, monospace"
fontSize:
  xs: "0.75rem"
  base: "1rem"
  xl: "1.25rem"
  2xl: "1.5rem"
```

**spacing.yml**

```yaml
# Example structure — 4px base scale
spacing:
  0: "0"
  1: "0.25rem" # 4px
  2: "0.5rem" # 8px
  4: "1rem" # 16px
  8: "2rem" # 32px
```

### Component Library (design/component-library.md)

Every project must maintain a component inventory documenting:

- Component name and purpose
- Props/API surface
- States (loading, empty, error, success)
- Accessibility considerations
- Usage examples

## Adapter Files

`CLAUDE.md`, `AI-AGENTS.md`, and `.github/copilot-instructions.md` are **generated files**. Do not edit them directly. They are produced from the KayaEOS adapter system using canonical sources (constitution, playbooks, agent catalog).

See `adapters/` in the KayaEOS repository for the generator specifications.

## CI/CD Requirements

Minimum CI pipeline for every project:

1. **Lint** — Prettier + ESLint (or equivalent)
2. **Type check** — TypeScript strict mode (or equivalent)
3. **Unit tests** — All must pass
4. **Build** — Must succeed
5. **Accessibility lint** — axe-core or equivalent

All checks are blocking on PR merge to main.
