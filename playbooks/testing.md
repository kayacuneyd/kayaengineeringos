---
id: PLBOOK-005
title: Testing
version: 1.0.0
status: active
agent: tester
triggers:
  - "test"
  - "spec"
  - "coverage"
  - "unit test"
  - "integration test"
  - "e2e test"
  - "write tests"
---

# Testing

> Write meaningful tests that verify behavior, prevent regressions, and serve as living documentation.

## Prerequisites

- [ ] The code to test is stable (not in flux)
- [ ] Expected behavior is documented or well understood
- [ ] Testing framework and tools are set up in the project

## Workflow

### Phase 1: Test Strategy

1. Determine test criticality based on the feature's risk:
   - **High** (auth, payments, data integrity): Unit + Integration + E2E
   - **Medium** (core features): Unit + Integration
   - **Low** (cosmetic, static content): Unit
2. Identify what to test:
   - Happy path: expected usage
   - Error path: invalid inputs, network failures, server errors
   - Edge cases: empty data, boundary values, race conditions
   - States: loading, empty, error, success
3. Do NOT test: implementation details, framework internals, third-party library behavior

**Checkpoint**: You have a clear test plan. You know what to test and at what level.

### Phase 2: Write Tests

1. Follow AAA pattern: **Arrange** → **Act** → **Assert**
2. Write test descriptions that explain behavior, not implementation:
   - ❌ Bad: "it calls handleSubmit"
   - ✅ Good: "it submits the form and shows a success message"
3. One assertion concept per test (not strictly one assert, but one behavior)
4. Use realistic data, not "foo", "bar", "test@test.com"
5. For UI components: test what the user sees and does, not internal state
6. For async: test loading state, success state, error state

**Checkpoint**: Tests are clear, readable, and test behavior.

### Phase 3: Verify

1. Run the tests — all must pass
2. Verify tests fail when the behavior changes (not false positives)
3. Check coverage — but don't obsess over 100%
4. Focus on uncovered critical paths, not uncovered lines
5. Ensure tests are fast (< 5 seconds for the full unit suite is ideal)

**Checkpoint**: Tests are reliable, meaningful, and fast.

### Phase 4: Maintain

1. Run tests before every commit (locally)
2. Tests must pass in CI — blocking on failure
3. Update tests when behavior changes intentionally
4. Delete tests that no longer test anything meaningful
5. If a bug escapes, the first fix is a test that catches it

**Checkpoint**: Test suite remains healthy and trustworthy.

## Quality Gates

- [ ] Tests cover happy path AND error path
- [ ] Tests cover all states (loading, empty, error, success)
- [ ] Tests describe behavior, not implementation
- [ ] Tests are deterministic (no flaky tests)
- [ ] All tests pass
- [ ] Critical paths have adequate coverage

## Outputs

- Unit tests (always)
- Integration tests (for medium+ criticality)
- E2E tests (for high criticality)
- Updated test documentation if new patterns introduced

## Related Playbooks

- [Build Feature](build-feature.md) — Tests are part of implementation
- [Bug Fix](bug-fix.md) — Regression tests
- [Code Review](code-review.md) — Review includes test quality check

## Related Agents

- [Tester](../agents/tester.md) — Primary agent
- [Implementer](../agents/implementer.md) — Writes tests alongside code
