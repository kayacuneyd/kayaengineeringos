---
id: PLBOOK-007
title: Deployment
version: 1.0.0
status: active
agent: implementer
triggers:
  - "deploy"
  - "release"
  - "ship"
  - "production"
  - "publish"
---

# Deployment

> Deploy code to production safely, with rollback capability and post-deployment verification.

## Prerequisites

- [ ] All tests pass on the release branch
- [ ] All CI checks are green
- [ ] Code review is approved
- [ ] CHANGELOG.md is updated
- [ ] Version is bumped according to SemVer
- [ ] Breaking changes have migration guides (if applicable)

## Workflow

### Phase 1: Pre-Deployment Checklist

1. Verify the release branch is up to date with main
2. Run the full test suite one final time
3. Check for any unresolved security advisories in dependencies
4. Verify environment variables are set correctly for production
5. Check database migration scripts (if applicable): are they reversible?
6. Verify rollback plan: can we go back to the previous version in < 5 minutes?
7. Notify the team about the impending deployment (if team project)

**Checkpoint**: Everything is verified. Rollback plan is ready. Team is notified.

### Phase 2: Deploy

1. Execute the deployment (manual or automated via CI/CD)
2. Monitor deployment logs in real-time
3. Watch for errors, crashes, or anomalies during deployment
4. Verify database migrations run successfully (if applicable)

**Checkpoint**: Deployment completed without errors. Application is serving traffic.

### Phase 3: Post-Deployment Verification

1. Smoke test critical paths:
   - Can users log in?
   - Can users perform core actions?
   - Are API endpoints responding?
   - Is the database accessible?
2. Monitor error tracking for 15 minutes post-deploy
3. Check performance metrics (LCP, FID, CLS) — no regression
4. Verify all third-party integrations are working
5. Check log streams for unexpected errors

**Checkpoint**: Production is healthy. No regressions detected. Users are unaffected.

### Phase 4: Communicate

1. Mark the release in GitHub Releases with changelog
2. Tag the release commit
3. Notify the team: deployment successful, what was released
4. If any issues found during verification:
   - Decide: rollback or hotfix?
   - If rollback: execute rollback plan, notify team, investigate
   - If hotfix: follow [Bug Fix](bug-fix.md) with urgent priority

**Checkpoint**: Release is documented and communicated.

## Quality Gates

- [ ] All tests pass
- [ ] CI/CD pipeline is green
- [ ] CHANGELOG.md updated
- [ ] Version bumped correctly
- [ ] Smoke tests pass on production
- [ ] No performance regression
- [ ] Rollback plan documented and tested
- [ ] Team notified

## Outputs

- Deployed application (production)
- GitHub Release with changelog
- Git tag for the release

## Related Playbooks

- [Bug Fix](bug-fix.md) — If post-deployment issues require a hotfix
- [Security Review](security-review.md) — Required before major releases
- [ADR Creation](adr-creation.md) — If deployment strategy changes

## Related Agents

- [Implementer](../agents/implementer.md) — Executes deployment
- [Security](../agents/security.md) — Pre-deployment security check
