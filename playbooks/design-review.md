---
id: PLBOOK-010
title: Design Review
version: 1.0.0
status: active
agent: designer
triggers:
  - "design review"
  - "UI review"
  - "UX review"
  - "visual review"
  - "review design"
  - "review UI"
---

# Design Review

> Audit implemented UI against design specifications, accessibility standards, and visual quality criteria.

## Prerequisites

- [ ] UI is implemented and visible (local dev server, staging, or PR preview)
- [ ] Design specification or component spec is available
- [ ] Design tokens are defined for the project

## Workflow

### Phase 1: Visual Consistency

Compare implementation against the design specification:

1. Check that design tokens are used correctly:
   - Colors match the token palette (no hardcoded hex values in components)
   - Spacing follows the spacing scale
   - Typography follows the type scale
2. Check component states:
   - All interactive states are implemented (hover, focus, active, disabled)
   - Loading states exist and look correct
   - Empty states exist and are user-friendly
   - Error states are clear and helpful
3. Check visual hierarchy:
   - Most important element is visually prominent
   - Information flows logically from top to bottom
   - White space is used intentionally

**Checkpoint**: Implementation matches the design spec. Tokens are used consistently.

### Phase 2: Responsive Design

1. Test at minimum supported width (375px mobile):
   - No horizontal scroll
   - Content is readable without zooming
   - Touch targets are at least 44x44px
2. Test at tablet width (768px):
   - Layout adapts appropriately
   - Navigation is usable
3. Test at desktop width (1280px+):
   - Content doesn't stretch unreasonably
   - Max-width constraints are applied
4. Test at intermediate widths — no broken layouts

**Checkpoint**: UI works at all breakpoints. Mobile-first is respected.

### Phase 3: Accessibility

Run automated and manual checks:

1. Run axe-core or Lighthouse accessibility audit — address all violations
2. Keyboard navigation:
   - Tab through all interactive elements
   - Tab order is logical
   - Focus is always visible (no `outline: none` without replacement)
   - Modals trap focus correctly
   - ESC closes modals and dropdowns
3. Screen reader:
   - Images have meaningful alt text (or empty for decorative)
   - Form inputs have associated labels
   - Error messages are announced (use `role="alert"`)
   - Dynamic content changes are announced (use `aria-live`)
4. Color contrast:
   - All text meets 4.5:1 (normal) or 3:1 (large) ratio
   - Information is never conveyed by color alone
5. Motion:
   - Animations respect `prefers-reduced-motion`
   - No flashing content that could trigger seizures

**Checkpoint**: Zero accessibility violations. WCAG AA compliance confirmed.

### Phase 4: UX Quality

1. **Clarity**: Can a new user understand what to do within 5 seconds?
2. **Efficiency**: Can a returning user complete the main action quickly?
3. **Error prevention**: Are destructive actions confirmed?
4. **Error recovery**: Are error messages clear and actionable?
5. **Feedback**: Does every action provide immediate visual feedback?
6. **Consistency**: Do similar elements behave the same way across the app?
7. **Copy**: Is all text clear, concise, and free of jargon?

**Checkpoint**: UX is intuitive, forgiving, and consistent.

### Phase 5: Dark Mode (if applicable)

1. Toggle dark mode — all content must be readable
2. Check contrast ratios in both modes
3. Ensure images and icons work on dark backgrounds
4. Verify that system preference detection works

**Checkpoint**: Dark mode is usable and visually coherent.

### Phase 6: Report

1. Categorize findings:
   - **Blocking**: Visual bugs, a11y violations, broken responsive behavior
   - **Important**: Inconsistencies with design spec, poor UX
   - **Nitpick**: Minor visual refinements
2. For each finding: screenshot, description, suggested fix
3. Approve only when blocking findings are resolved

**Checkpoint**: Design review is complete with clear, actionable feedback.

## Quality Gates

- [ ] Design tokens used consistently (no hardcoded values)
- [ ] All component states implemented correctly
- [ ] Responsive at all breakpoints (mobile, tablet, desktop)
- [ ] WCAG AA accessibility — zero violations
- [ ] Keyboard navigation works end to end
- [ ] Screen reader announces content correctly
- [ ] UX is intuitive and consistent
- [ ] Dark mode functional (if applicable)
- [ ] All blocking findings resolved

## Outputs

- Design review report with categorized findings
- Screenshots of issues (if applicable)
- Approval or change request

## Related Playbooks

- [UI Design](ui-design.md) — What the design should have followed
- [Code Review](code-review.md) — Design review is part of the broader review
- [Build Feature](build-feature.md) — The implementer's workflow

## Related Agents

- [Designer](../agents/designer.md) — Primary agent
- [Reviewer](../agents/reviewer.md) — Ensures design feedback is addressed
