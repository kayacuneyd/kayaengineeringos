# KayaEOS — Engineering Operating System

This project follows **KayaEOS** — a model-agnostic, version-controlled engineering framework for AI-assisted development.

## Core Principles (from Engineering Constitution)

1. **Design First**: Start every feature with design — component tree, states, design tokens. Never hardcode visual values.
2. **Simplicity Over Complexity**: YAGNI. Single responsibility. 3-pass readability rule.
3. **Quality Gates**: No untested code. Code review mandatory. Lint/format blocking in CI.
4. **Documentation Lives with Code**: README-driven. ADR for every significant decision. Comments explain WHY, not WHAT.
5. **Progressive Enhancement**: Mobile-first, responsive-required. WCAG AA accessibility minimum.
6. **AI-Assisted, Human-Responsible**: AI generates → Human reviews → Human understands → Human ships.
7. **All States Matter**: Every component handles loading, empty, error, success, and edge cases.
8. **Design Tokens Over Hardcoded Values**: Always use tokens for colors, spacing, typography.

Full constitution: `constitution.md`

## How to Use Playbooks

Playbooks are loaded on demand using trigger keywords. When a task matches a trigger, load the playbook:

| Playbook        | File                           | Trigger Keywords                                    |
| --------------- | ------------------------------ | --------------------------------------------------- |
| Build Feature   | `playbooks/build-feature.md`   | feature, implement, build, develop                  |
| Bug Fix         | `playbooks/bug-fix.md`         | bug, fix, debug, issue, error                       |
| Refactor        | `playbooks/refactor.md`        | refactor, clean up, simplify, tech debt             |
| Code Review     | `playbooks/code-review.md`     | review, PR, pull request, code review               |
| Testing         | `playbooks/testing.md`         | test, spec, coverage, unit test                     |
| ADR Creation    | `playbooks/adr-creation.md`    | ADR, architecture decision, decision                |
| Deployment      | `playbooks/deployment.md`      | deploy, release, ship, production                   |
| Security Review | `playbooks/security-review.md` | security, vulnerability, auth, CVE                  |
| UI Design       | `playbooks/ui-design.md`       | design, UI, UX, component, interface, layout, style |
| Design Review   | `playbooks/design-review.md`   | design review, UI review, review design             |
| Design-to-Code  | `playbooks/design-to-code.md`  | design to code, implement design, figma to code     |

**To use a playbook:** Reference it directly in your request.
Example: `@playbooks/build-feature.md follow this playbook to implement user login`

## Agent Definitions

Agents define role-specific behaviors. Load them when switching contexts:

| Agent       | File                    | Role                                   |
| ----------- | ----------------------- | -------------------------------------- |
| Architect   | `agents/architect.md`   | System design and ADRs                 |
| Implementer | `agents/implementer.md` | Feature implementation and bug fixing  |
| Reviewer    | `agents/reviewer.md`    | Code and quality review                |
| Tester      | `agents/tester.md`      | Test strategy and QA                   |
| Security    | `agents/security.md`    | Security audit and vulnerabilities     |
| Docs        | `agents/docs.md`        | Documentation and knowledge management |
| Designer    | `agents/designer.md`    | UI/UX design and visual quality        |

## ADR System

Architecture Decision Records are in `adr/`. Check `adr/INDEX.md` before making architectural changes.
Create an ADR for every significant decision using `adr/_template.md`.

## Design Tokens

When working on UI, always reference design tokens from `design/tokens/`. Never hardcode:

- Colors → use token variables
- Spacing → use spacing scale
- Typography → use type scale

## Memory & Retrieval

This file is the context index (~500 tokens). Full playbook content is loaded on demand.
Do NOT load the entire framework. Load only what this task needs.
For details on this convention, see `memory-retrieval.md`.

## Commit Convention

Use Conventional Commits:

```
feat: description
fix: description
refactor: description
docs: description
test: description
```

## CI Gates (all blocking)

1. Lint (zero warnings)
2. Type check (strict mode)
3. Unit tests (all pass)
4. Build (succeeds)
5. Accessibility audit (zero violations)

---

_Generated from KayaEOS canonical sources. Do not edit manually._
_Version: 1.0.0 | Generated: 2026-07-19_
