---
id: PLBOOK-002
title: Bug Fix
version: 1.0.0
status: active
agent: implementer
triggers:
  - "bug"
  - "fix"
  - "debug"
  - "issue"
  - "error"
  - "problem"
---

# Bug Fix

> Diagnose, fix, and verify a bug following a systematic debugging workflow.

## Prerequisites

- [ ] Bug report exists with steps to reproduce
- [ ] Expected behavior is documented
- [ ] Actual behavior is documented
- [ ] Environment details are captured (browser, OS, version, etc.)

## Workflow

### Phase 1: Reproduce

1. Read the bug report thoroughly
2. Reproduce the bug using the reported steps
3. If unreproducible, ask for more details or environment information
4. Document the minimal reproduction steps
5. Identify the scope: what systems, components, or modules are affected?

**Checkpoint**: Bug is reliably reproducible. You can trigger it on demand.

### Phase 2: Diagnose

1. Form a hypothesis about the root cause
2. Use debugging tools (breakpoints, logs, devtools) to verify or disprove the hypothesis
3. Trace the code path from input to failure point
4. If stuck: check recent changes (git log, blame), check related ADRs
5. Only when the root cause is confirmed, move to fix phase

**Checkpoint**: Root cause is identified and confirmed through debugging, not guessing.

### Phase 3: Fix

1. Write a failing test that reproduces the bug (if not already covered)
2. Implement the minimal fix
3. Verify the test now passes
4. Check for side effects: does the fix break anything else?
5. Run the full test suite — all tests must pass
6. Consider if this bug reveals a systemic issue (update playbooks if yes)

**Checkpoint**: Bug is fixed. Regression test passes. No side effects detected.

### Phase 4: Prevent

1. Add or update tests to prevent regression
2. Consider: could this bug happen in similar places? If yes, fix those too or create follow-up issues
3. If the bug was caused by unclear code, refactor for clarity (chain to refactor playbook)
4. If the bug was caused by missing documentation, update docs

**Checkpoint**: Bug cannot recur. Tests cover the regression case.

### Phase 5: Ship

1. Write a conventional commit message explaining the fix
2. Create a PR referencing the bug report
3. Include: what caused it, the fix, and why this fix (not just what changed)
4. Request review
5. Merge after approval

**Checkpoint**: Fix is merged. Bug report is closed.

## Quality Gates

- [ ] Bug is reliably reproducible before fix
- [ ] Root cause is confirmed, not guessed
- [ ] Regression test is in place
- [ ] Full test suite passes
- [ ] Side effects checked and none found
- [ ] Code review approved

## Outputs

- Minimal fix code
- Regression test(s)
- Updated docs (if bug was caused by undocumented behavior)
- Follow-up issues (if systemic issue found)

## Related Playbooks

- [Code Review](code-review.md) — Required before merge
- [Refactor](refactor.md) — If bug was caused by unclear code
- [Testing](testing.md) — For test strategy

## Related Agents

- [Implementer](../agents/implementer.md) — Diagnosis and fix
- [Reviewer](../agents/reviewer.md) — Code review
- [Tester](../agents/tester.md) — Verification
