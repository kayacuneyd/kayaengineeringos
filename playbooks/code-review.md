---
id: PLBOOK-004
title: Code Review
version: 1.0.0
status: active
agent: reviewer
triggers:
  - "review"
  - "PR"
  - "pull request"
  - "code review"
  - "review code"
---

# Code Review

> Systematically review code for correctness, simplicity, consistency, and adherence to KayaEOS standards.

## Prerequisites

- [ ] PR description explains WHAT and WHY (not HOW)
- [ ] All CI checks are green (tests, lint, type check, build)
- [ ] PR is appropriately sized (reviewable in one sitting, < 400 lines changed ideally)
- [ ] Linked issues or specs are referenced

## Workflow

### Phase 1: Context

1. Read the PR description — understand the goal
2. Review linked issues, specs, or ADRs for full context
3. Check out the branch and verify it builds/runs locally
4. Understand the scope: what files, what modules, what layers are touched?

**Checkpoint**: You understand what this PR is trying to achieve.

### Phase 2: Review for Correctness

1. Does the code do what the PR description claims?
2. Are edge cases handled? (loading, empty, error, success states)
3. Is input validated and sanitized?
4. Are error states handled gracefully?
5. Are there any obvious race conditions or timing issues?
6. For UI: does it work on mobile, tablet, desktop?

**Checkpoint**: You are confident the code is functionally correct.

### Phase 3: Review for Quality

Check against KayaEOS Engineering Constitution principles:

1. **Simplicity**: Could this be simpler? Is there unnecessary abstraction?
2. **Single Responsibility**: Does each function/component/module have one reason to change?
3. **Readability (3-Pass Rule)**: Can you understand WHAT, HOW, and WHY?
4. **Naming**: Are names clear and consistent with project conventions?
5. **No dead code**: Debug logs, commented-out code, unused imports?
6. **No magic values**: Constants used instead of inline literals?
7. **DRY**: Any duplication that should be extracted? (But respect the 3-occurrence rule)

**Checkpoint**: Code meets KayaEOS quality standards.

### Phase 4: Review for Testing

1. Are there tests for the changed code?
2. Do the tests cover happy path AND edge cases?
3. Do the tests actually test the right thing? (Not just coverage padding)
4. For bug fixes: is there a regression test?
5. Are test descriptions clear about what is being tested?

**Checkpoint**: Testing is adequate and meaningful.

### Phase 5: Review for Consistency

1. Does this code follow existing project patterns?
2. Are design tokens used instead of hardcoded values? (UI)
3. Is the code style consistent with the rest of the codebase?
4. Are conventions from the project's ADRs followed?
5. Are new patterns introduced? If yes, is there documentation?

**Checkpoint**: Code integrates seamlessly with the existing codebase.

### Phase 6: Review for Accessibility (UI)

1. Are all interactive elements keyboard accessible?
2. Are ARIA labels present where needed?
3. Is color contrast sufficient? (4.5:1 normal, 3:1 large)
4. Do screen readers receive meaningful content?
5. Is focus management correct (modals, navigation)?

**Checkpoint**: UI meets WCAG AA standards.

### Phase 7: Deliver Review

1. Categorize feedback:
   - **Blocking**: Must fix before merge (bugs, security, a11y violations)
   - **Important**: Should fix (clarity, consistency, missing tests)
   - **Nitpick**: Optional (naming preferences, minor style)
2. Be specific: point to the exact line, explain WHY it's an issue, suggest a fix
3. Approve only when all blocking and important feedback is resolved

**Checkpoint**: Review is delivered clearly and constructively.

## Quality Gates (for the Review Itself)

- [ ] Every changed file has been reviewed
- [ ] Correctness verified
- [ ] Quality standards verified
- [ ] Testing is adequate
- [ ] Consistency with codebase confirmed
- [ ] Accessibility checked (UI changes)
- [ ] Feedback is clear, actionable, and categorized

## Outputs

- Approved PR (if all checks pass)
- Constructive, actionable review feedback (if changes needed)

## Related Playbooks

- [Build Feature](build-feature.md) — What the implementer should have followed
- [Bug Fix](bug-fix.md) — Review context for bug fix PRs
- [Refactor](refactor.md) — Review context for refactor PRs
- [Security Review](security-review.md) — If PR touches auth or sensitive data
- [Testing](testing.md) — Test quality standards

## Related Agents

- [Reviewer](../agents/reviewer.md) — Primary agent
- [Security](../agents/security.md) — If security-sensitive
- [Designer](../agents/designer.md) — If UI changes
