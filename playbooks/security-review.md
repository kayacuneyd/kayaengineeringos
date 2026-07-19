---
id: PLBOOK-008
title: Security Review
version: 1.0.0
status: active
agent: security
triggers:
  - "security"
  - "vulnerability"
  - "auth"
  - "CVE"
  - "security review"
  - "security audit"
---

# Security Review

> Audit code, configuration, and dependencies for security vulnerabilities before merging or deploying.

## Prerequisites

- [ ] Code changes are complete and in PR
- [ ] Dependency list is available (package.json, requirements.txt, etc.)
- [ ] Environment variable schema is documented

## When to Trigger

A security review is ALWAYS required when changes touch:

- Authentication or authorization logic
- Password handling, session management, or token management
- Database queries (SQL injection risk)
- API endpoints with write/delete access
- File upload or user-generated content handling
- Personal Identifiable Information (PII) processing
- Payment processing or financial data
- Third-party integrations with access to internal systems
- Configuration that exposes new ports or services

## Workflow

### Phase 1: Scope

1. Identify all files changed in the PR
2. Determine which security domains are affected
3. Identify data flows: where does user input enter? Where does sensitive data exit?

**Checkpoint**: You know exactly what to audit.

### Phase 2: Audit Code

Check for the following vulnerabilities:

1. **Injection**: SQL, NoSQL, command, LDAP injection
   - Are all user inputs parameterized?
   - Are ORMs used correctly (no raw queries with string interpolation)?
2. **Authentication**: Is auth properly enforced?
   - Are protected routes actually protected?
   - Is session/token management secure (HTTPOnly, Secure, SameSite)?
3. **Authorization**: Are permissions checked server-side?
   - Can a user access another user's data by changing an ID?
   - Are admin endpoints properly restricted?
4. **Data Exposure**:
   - Is sensitive data ever logged?
   - Are error messages revealing stack traces or internal paths?
   - Is PII properly masked or encrypted?
5. **Input Validation**:
   - Is all user input validated on BOTH client and server?
   - Are file uploads restricted by type, size, and content?
6. **CSRF/XSS**:
   - Are forms protected against CSRF?
   - Is user-generated content sanitized before rendering?
   - Is CSP (Content Security Policy) configured?
7. **Dependencies**:
   - Are there known vulnerabilities in dependencies?
   - Are all dependencies at their latest secure versions?
8. **Secrets**:
   - Are any secrets, keys, or tokens in the code?
   - Check for accidental commits of .env files

**Checkpoint**: All code paths audited. Vulnerabilities identified.

### Phase 3: Report

For each finding, document:

- **Severity**: Critical / High / Medium / Low
- **Location**: File and line number
- **Description**: What's the vulnerability?
- **Impact**: What could an attacker do?
- **Fix**: How to resolve it?

**Critical and High** severity findings are BLOCKING. Must be fixed before merge.
**Medium** severity findings should be fixed or have a tracked follow-up issue.
**Low** severity findings are informational.

**Checkpoint**: All findings documented with clear fix instructions.

### Phase 4: Verify Fixes

1. Review the applied fixes
2. Verify the vulnerability is actually resolved (not just hidden)
3. Check that the fix doesn't introduce new issues
4. Run dependency audit to confirm clean bill of health

**Checkpoint**: All blocking findings resolved. Security review approved.

## Quality Gates

- [ ] All code paths in scope audited
- [ ] No secrets in code or commit history
- [ ] Dependencies are free of known vulnerabilities
- [ ] Input validation exists on both client and server
- [ ] Authentication and authorization properly enforced
- [ ] Sensitive data is not exposed in logs or errors
- [ ] Critical and High findings are resolved
- [ ] Security review approved

## Outputs

- Security review report (as PR comments or separate document)
- List of resolved findings
- Follow-up issues for non-blocking findings

## Related Playbooks

- [Code Review](code-review.md) — Security review is part of the broader review process
- [Deployment](deployment.md) — Security check before deploying
- [Bug Fix](bug-fix.md) — If a security vulnerability is found in production

## Related Agents

- [Security](../agents/security.md) — Primary agent
- [Reviewer](../agents/reviewer.md) — Ensures security findings are addressed
- [Implementer](../agents/implementer.md) — Applies fixes
