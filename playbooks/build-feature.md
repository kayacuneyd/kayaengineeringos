---
id: PLBOOK-001
title: Build Feature
version: 1.0.0
status: active
agent: implementer
triggers:
  - "feature"
  - "implement"
  - "build"
  - "develop"
  - "new feature"
  - "feature implementation"
---

# Build Feature

> Implement a new feature from specification to merged code, following KayaEOS quality standards.

## Prerequisites

- [ ] Feature specification exists (in docs/ or as an ADR)
- [ ] Design tokens are defined (for UI features)
- [ ] Component tree is mapped (for UI features)
- [ ] Acceptance criteria are documented

## Workflow

### Phase 1: Understand and Plan

1. Read the feature specification thoroughly
2. Identify all acceptance criteria
3. Map the affected code areas (files, components, modules)
4. Break down the feature into implementable units (tasks)
5. Identify edge cases: loading, empty, error, success, and boundary states
6. For UI features, reference design tokens and component library

**Checkpoint**: You can explain the feature to someone else in 60 seconds. If not, re-read the spec.

### Phase 2: Implement

1. Write or update tests for the first unit (TDD: test first, then code)
2. Implement the code to make the test pass
3. Refactor for clarity and consistency while tests stay green
4. Repeat for each unit
5. Handle all states: loading, empty, error, success, edge cases
6. For UI: implement mobile-first, then enhance for larger breakpoints
7. For UI: ensure keyboard navigation and screen reader support

**Checkpoint**: All units implemented. All tests green. Lint passes with zero warnings.

### Phase 3: Polish

1. Run the full test suite — all tests must pass
2. Run lint and formatter — zero warnings, zero errors
3. Run type checker — zero errors (strict mode if available)
4. For UI: run accessibility audit (axe-core or equivalent) — zero violations
5. Self-review the diff: look for dead code, debug logs, commented-out code
6. Verify against acceptance criteria — every criterion met
7. Update or create documentation if the feature adds new patterns

**Checkpoint**: Diff is clean. All checks pass. Every acceptance criterion is satisfied.

### Phase 4: Ship

1. Write a clear, conventional commit message
2. Create a PR with a description that explains WHAT and WHY (not HOW — the code shows HOW)
3. Request review from the appropriate agent (reviewer)
4. Address all review feedback
5. Merge only after approval and all CI checks pass

**Checkpoint**: PR merged to main. Feature is live.

## Quality Gates

- [ ] All unit tests pass
- [ ] All integration tests pass (if applicable)
- [ ] E2E tests pass (if high-criticality feature)
- [ ] Lint passes with zero warnings
- [ ] Type checker passes with zero errors
- [ ] Accessibility audit passes (WCAG AA, if UI feature)
- [ ] Code review approved
- [ ] CI pipeline green

## Outputs

- Implemented feature code
- Unit tests (required)
- Integration tests (if applicable)
- Updated component library docs (if new components created)
- ADR (if architectural decision was made)

## Related Playbooks

- [Code Review](code-review.md) — Required before merge
- [Testing](testing.md) — For test strategy details
- [UI Design](ui-design.md) — For UI-intensive features
- [ADR Creation](adr-creation.md) — If architectural decisions were made

## Related Agents

- [Implementer](../agents/implementer.md) — Primary agent for this workflow
- [Reviewer](../agents/reviewer.md) — Code review
- [Designer](../agents/designer.md) — UI review (if applicable)
