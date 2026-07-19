# KayaEOS — Engineering Operating System

> Model-agnostic, version-controlled engineering framework for AI-assisted software development.

## Engineering Constitution

All development follows the KayaEOS Engineering Constitution (`constitution.md`):

1. **Design First** — Component tree, states, and design tokens before code
2. **Simplicity Over Complexity** — YAGNI, single responsibility, 3-pass readability
3. **Quality Gates** — No untested code, mandatory review, linting blocking in CI
4. **Documentation Drives Development** — README-driven, ADR for decisions, comments explain WHY
5. **Progressive Enhancement** — Mobile-first, WCAG AA accessibility, graceful degradation
6. **AI-Assisted, Human-Responsible** — AI generates, human reviews, understands, and ships
7. **All States Matter** — Loading, empty, error, success, and edge cases for every component
8. **Design Tokens Over Hardcoded Values** — Colors, spacing, typography always from tokens

## Available Agents

Load the appropriate agent definition when switching contexts:

| Agent       | Definition File           | Activated By                                      |
| ----------- | ------------------------- | ------------------------------------------------- |
| Architect   | `agents/architect.md`     | architecture, system design, ADR, decision        |
| Implementer | `agents/implementer.md`   | implement, build, develop, fix, bug, refactor     |
| Reviewer    | `agents/reviewer.md`      | review, PR, pull request, code review             |
| Tester      | `agents/tester.md`        | test, spec, coverage, QA                          |
| Security    | `agents/security.md`      | security, vulnerability, auth, CVE                |
| Docs        | `agents/docs.md`          | document, docs, documentation, readme             |
| Designer    | `agents/designer.md`      | design, UI, UX, visual, component, interface      |

Each agent definition includes: role, responsibilities, core principles, default playbooks, and handoff conventions.

## Playbook Library

Playbooks are loaded on demand. Match trigger keywords against the user's request:

| Playbook        | File                           | When to Load                                       |
| --------------- | ------------------------------ | -------------------------------------------------- |
| Build Feature   | `playbooks/build-feature.md`   | New feature implementation, building, developing   |
| Bug Fix         | `playbooks/bug-fix.md`         | Debugging, fixing issues, error resolution         |
| Refactor        | `playbooks/refactor.md`        | Code cleanup, restructuring, simplifying           |
| Code Review     | `playbooks/code-review.md`     | PR review, code inspection                         |
| Testing         | `playbooks/testing.md`         | Writing or updating tests, test strategy           |
| ADR Creation    | `playbooks/adr-creation.md`    | Architectural decisions, creating ADRs             |
| Deployment      | `playbooks/deployment.md`      | Releasing, shipping, production deployment         |
| Security Review | `playbooks/security-review.md` | Security auditing, vulnerability assessment        |
| UI Design       | `playbooks/ui-design.md`       | Designing interfaces, components, layouts          |
| Design Review   | `playbooks/design-review.md`   | Reviewing implemented UI against design specs      |
| Design-to-Code  | `playbooks/design-to-code.md`  | Converting design specs/screenshots to code        |

## ADR System

Architecture Decision Records in `adr/`:
- Browse: `adr/INDEX.md`
- Create new: use `adr/_template.md`
- ADRs are the project's long-term memory for WHY decisions were made

## Design System

Projects following KayaEOS must use design tokens from `design/tokens/`:
- `colors.yml` — Color palette (primary, neutral, semantic)
- `typography.yml` — Font families and type scale
- `spacing.yml` — Spacing scale (4px base)

No hardcoded values in UI code. Everything references a token.

## Memory & Retrieval Convention

This file serves as the context index (~500 tokens). It is always loaded.

**Do not load the entire framework.** When a task matches trigger keywords, load only the relevant playbook(s) and agent definition(s). This keeps token costs minimal while providing comprehensive guidance.

Full convention: `memory-retrieval.md`

## Quality Gates (CI)

Every PR must pass before merge:
1. Lint — zero warnings
2. Type check — strict mode, zero errors
3. Unit tests — all pass
4. Build — succeeds
5. Accessibility audit — zero violations (UI changes)

All gates are blocking.

## Commit Convention

Conventional Commits: `feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`

## Repository Structure

Follow the KayaEOS Repository Blueprint (`blueprint.md`):
- `design/tokens/` — Design tokens
- `adr/` — Architecture Decision Records
- `playbooks/` — Workflow definitions
- `agents/` — Agent definitions
- `docs/` — Project documentation
- `src/` — Source code
- `tests/` — Test files

---

_Generated from KayaEOS canonical sources. Do not edit manually._
_Version: 1.0.0 | Generated: 2026-07-19_