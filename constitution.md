---
id: kaya-eos-constitution
title: KayaEOS Engineering Constitution
version: 1.0.0
status: active
author: Cüneyt Kaya
created: 2026-07-19
updated: 2026-07-19
---

# KayaEOS Engineering Constitution v1

> The immutable engineering principles that govern all KayaEOS-compliant projects. Think of this as the constitution — all playbooks, agents, and workflows derive from, and must not contradict, these principles.

---

## 1. Design First

Design is not an afterthought. It is the foundation.

### 1.1 Start Every Feature with Design

Before writing a single line of code, define:

- **Component tree**: What components exist, how they compose
- **State transitions**: Loading → Empty → Error → Success → Edge cases
- **User flow**: Happy path AND all alternative paths
- **Design tokens**: Colors, typography, spacing, shadows, radii — defined as tokens, not hardcoded values

### 1.2 Component-First Thinking

Every UI element is a component. Components are:

- **Composable**: Smaller components combine into larger ones
- **Reusable**: Same component, different context, same behavior
- **Testable**: Each component can be tested in isolation
- **Accessible**: Every component meets WCAG AA minimum

### 1.3 Steve Jobs Principle

> "Design is not just what it looks like and feels like. Design is how it works."

Apply this principle to everything:

- API design: The interface IS the design
- Code structure: Readability IS the design
- Error messages: Clarity IS the design
- Documentation: Discoverability IS the design

### 1.4 Design Tokens Over Hardcoded Values

```yaml
# ✅ Correct — use design tokens
color: var(--color-primary-500)
spacing: var(--spacing-4)

# ❌ Wrong — hardcoded values
color: #3B82F6
spacing: 16px
```

Every project must define and consume design tokens. No exceptions.

---

## 2. Simplicity Over Complexity

### 2.1 YAGNI (You Ain't Gonna Need It)

Do not build features, abstractions, or infrastructure "just in case." Build what is needed now, design so it can be extended later.

### 2.2 The 3-Pass Rule

Write every piece of code as if it will be read three times:

1. First pass: Understand WHAT it does
2. Second pass: Understand HOW it does it
3. Third pass: Understand WHY it was done that way

If any pass fails, refactor.

### 2.3 Single Responsibility

Every function, class, component, module, and playbook must have ONE reason to change.

### 2.4 Avoid Premature Abstraction

Duplicate code twice. Abstract on the third occurrence. Not before.

---

## 3. Quality Gates

### 3.1 No Untested Code

Every feature ships with tests. The type and depth of testing depend on the criticality:

| Criticality           | Unit     | Integration | E2E      |
| --------------------- | -------- | ----------- | -------- |
| High (auth, payments) | Required | Required    | Required |
| Medium (features)     | Required | Required    | Optional |
| Low (cosmetic)        | Required | Optional    | Optional |

### 3.2 Code Review Is Mandatory

No code reaches main without review. The reviewer verifies:

- Correctness: Does it do what it claims?
- Simplicity: Could it be simpler?
- Consistency: Does it follow project conventions?
- Test coverage: Are the right things tested?
- Accessibility: Does it meet a11y standards?

### 3.3 Linting and Formatting Are Non-Negotiable

Automated. In CI. Blocking merge on failure.

### 3.4 Security Review for Sensitive Changes

Any change touching auth, data access, API endpoints with side effects, or PII must pass a security review.

---

## 4. Documentation Lives with Code

### 4.1 README-Driven Development

Every project starts with a README that answers:

- What is this?
- Why does it exist?
- How do I run it?
- How do I contribute?

### 4.2 ADR for Every Significant Decision

Architecture Decision Records (ADRs) capture the context, options considered, decision made, and consequences. See `adr/` system.

### 4.3 Self-Documenting Code First, Comments Second

Write code that explains itself. Use comments only to explain WHY, never WHAT.

```
// ❌ Bad — explains what
// increment counter by 1
counter += 1

// ✅ Good — explains why
// Reset on overflow to prevent counter wrapping
counter = (counter + 1) % MAX_VALUE
```

---

## 5. Progressive Enhancement

### 5.1 Mobile-First, Responsive-Required

Every UI component works on mobile first, then enhances for larger screens.

### 5.2 Graceful Degradation

Features that depend on JavaScript, network, or browser capabilities must function at a basic level without them.

### 5.3 Accessibility Is Not Optional

- WCAG AA minimum for all projects
- Keyboard navigation for all interactive elements
- Screen reader support for all content
- Sufficient color contrast (4.5:1 for normal text, 3:1 for large text)

---

## 6. AI-Assisted, Human-Responsible

### 6.1 AI Is a Tool, Not a Replacement

AI generates code, suggests solutions, and automates repetitive tasks. The human developer:

- Reviews every AI-generated line
- Understands every AI-suggested solution
- Takes full responsibility for the output

### 6.2 Context Is King

AI quality is directly proportional to context quality. Always provide:

- Relevant playbooks
- Existing code patterns
- Project constraints and conventions
- Design tokens and component library references

### 6.3 Iterate, Don't Generate-and-Ship

AI-generated code is a first draft. The workflow is:

1. AI generates → Human reviews and understands
2. Human refactors for clarity and consistency
3. Tests pass → Lint passes → Review → Merge

Never: AI generates → Copy-paste → Ship.

---

## 7. Continuous Improvement

### 7.1 Retrospective on Every Feature

After shipping a feature, ask:

- What went well?
- What slowed us down?
- What would we do differently?
- Does this change any of our conventions?

### 7.2 Playbook Evolution

Playbooks are living documents. If a playbook consistently leads to friction, update it. Every playbook change requires an ADR.

### 7.3 Tool-Agnostic Standards

Standards defined here must be implementable regardless of language, framework, or AI tool. If a standard only works with React, it doesn't belong here.

---

## 8. Security & Data Privacy

### 8.1 Never Trust User Input

Validate, sanitize, and escape. On both client and server. Always.

### 8.2 Secrets Never Touch Code

API keys, tokens, passwords, and credentials live in environment variables or secret managers. Never in source files. Never in commit history.

### 8.3 Principle of Least Privilege

Every service account, API key, and database user has the minimum permissions needed to function.

### 8.4 Dependency Hygiene

- Prefer well-maintained, widely-used dependencies
- Audit dependencies regularly
- Pin versions, not ranges
- Keep dependencies minimal

---

## 9. Performance

### 9.1 Measure Before Optimizing

No performance optimization without a measurement showing the problem.

### 9.2 Performance Budgets

Every project defines:

- **LCP (Largest Contentful Paint)**: < 2.5s
- **FID (First Input Delay)**: < 100ms
- **CLS (Cumulative Layout Shift)**: < 0.1

### 9.3 Bundle Size Awareness

- Know the cost of every dependency you add
- Lazy load by default, eager load only when necessary
- Images must be optimized and lazy-loaded

---

## 10. Versioning & Breaking Changes

### 10.1 Semantic Versioning

All projects and playbooks follow SemVer: MAJOR.MINOR.PATCH

### 10.2 Breaking Change Process

1. Document the change in an ADR
2. Deprecate the old behavior with a warning (one version before removal)
3. Provide migration guide
4. Remove in the next MAJOR version

### 10.3 Changelog

Every release includes a human-readable CHANGELOG.md following [Keep a Changelog](https://keepachangelog.com/) format.

---

## Amendment Process

This constitution can be amended through the following process:

1. Propose amendment via issue with label `constitution-amendment`
2. Discuss with at least 2 reviewers
3. If approved, create an ADR documenting the change
4. Update this document, incrementing MINOR version
5. Update all affected playbooks to align with the amendment

---

_This constitution is the foundation. All playbooks, agent definitions, and workflow engines derive their authority from these principles._
