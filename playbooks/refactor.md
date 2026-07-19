---
id: PLBOOK-003
title: Refactor
version: 1.0.0
status: active
agent: implementer
triggers:
  - "refactor"
  - "clean up"
  - "improve structure"
  - "restructure"
  - "simplify"
  - "tech debt"
---

# Refactor

> Improve code structure, readability, and maintainability without changing external behavior.

## Prerequisites

- [ ] The code to refactor has adequate test coverage
- [ ] The current behavior is well understood
- [ ] The refactoring goal is clear (performance, readability, modularity, etc.)
- [ ] An ADR exists if the refactor changes architectural patterns

## Workflow

### Phase 1: Baseline

1. Run the full test suite — confirm everything is green
2. Identify the specific code boundaries to refactor
3. Document the current behavior (what it does, not how)
4. Ensure all existing tests accurately capture current behavior
5. Add characterization tests for any untested behavior you'll touch

**Checkpoint**: Full test suite is green. You have a safety net for the refactor.

### Phase 2: Refactor

1. Make one small, verifiable change
2. Run tests — must stay green
3. Commit the change
4. Repeat until refactoring goal is achieved

Guiding principles during refactoring:

- Extract repeated code into shared utilities (3+ occurrences rule)
- Rename for clarity (variables, functions, components)
- Split large functions (> ~30 lines) into smaller, named functions
- Flatten deep nesting (> 3 levels)
- Replace magic numbers with named constants
- Simplify conditionals (early returns, guard clauses)
- Remove dead code, commented-out code, debug logs

**Checkpoint**: All tests still green. Code is structurally improved.

### Phase 3: Verify

1. Run the full test suite — all tests pass
2. Run lint and formatter — zero warnings
3. Run type checker — zero errors
4. Compare bundle size or performance metrics if applicable (must not regress)
5. Manual smoke test of affected functionality
6. Self-review: is the code simpler, more readable, more maintainable?

**Checkpoint**: No regressions. Code quality improved. All checks pass.

### Phase 4: Ship

1. Write a clear commit message describing the structural change
2. PR description: "before" vs "after" if structural change is significant
3. No change to external behavior — make this explicit in the PR
4. Request review
5. Merge after approval

**Checkpoint**: Refactored code merged. Zero behavior changes.

## Quality Gates

- [ ] Full test suite passes (same tests as before, no behavioral changes)
- [ ] No new functionality introduced (refactor only)
- [ ] Lint passes with zero warnings
- [ ] Type checker passes
- [ ] No performance regression
- [ ] Code review approved
- [ ] ADR created if architectural changes were made

## Outputs

- Refactored code (cleaner, more maintainable)
- Unchanged test suite (tests still pass)
- ADR (if architectural pattern changed)
- Updated playbooks (if refactor revealed better patterns)

## Related Playbooks

- [Code Review](code-review.md) — Required before merge
- [Testing](testing.md) — Ensure safety net is adequate
- [ADR Creation](adr-creation.md) — If architectural changes
- [Bug Fix](bug-fix.md) — If refactor reveals a bug (STOP refactor, switch to bug-fix)

## Related Agents

- [Implementer](../agents/implementer.md) — Primary agent
- [Reviewer](../agents/reviewer.md) — Code review
- [Architect](../agents/architect.md) — If structural patterns change
