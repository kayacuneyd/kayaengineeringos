---
id: PLBOOK-011
title: Design-to-Code
version: 1.0.0
status: active
agent: implementer
triggers:
  - "design to code"
  - "implement design"
  - "convert design"
  - "from design"
  - "screenshot to code"
  - "figma to code"
  - "mockup to code"
---

# Design-to-Code

> Convert a UI design (specification, screenshot, or Figma mockup) into production-ready, token-based, accessible frontend code.

## Prerequisites

- [ ] Design specification exists (component spec from [UI Design](ui-design.md), screenshot, or Figma link)
- [ ] Design tokens are defined for the project
- [ ] Component library/framework is chosen (shadcn/ui, Tailwind, MUI, custom, etc.)
- [ ] Target framework is known (React, Vue, Svelte, etc.)

## Context Checklist

Before writing code, ensure these are loaded into AI context:

- [ ] Design tokens (colors.yml, typography.yml, spacing.yml)
- [ ] Component library reference (component-library.md)
- [ ] Project coding conventions
- [ ] The design specification being implemented

## Workflow

### Phase 1: Analyze the Design

1. Identify all components in the design:
   - Which are existing components? (Reuse them)
   - Which are new compositions of existing components?
   - Which are entirely new components?
2. Map the component hierarchy (parent → children → grandchildren)
3. Identify data dependencies:
   - What data does each component need?
   - Where does the data come from? (props, API, context, route params?)
4. Map out all states: Loading, Empty, Error, Success, Edge cases

**Checkpoint**: Component tree and data flow are mapped. States are identified.

### Phase 2: Implement Structure (HTML First)

1. Start with semantic HTML — no styling yet:
   - Use correct semantic elements (`<nav>`, `<main>`, `<article>`, `<section>`, `<form>`)
   - Heading hierarchy is logical (h1 → h2 → h3, no skipped levels)
   - Interactive elements are `<button>`, `<a>`, `<input>` — not divs with onClick
2. Implement the component hierarchy from top to bottom
3. Pass placeholder data, not real API calls yet
4. Implement all states as separate variations or conditional renders

**Checkpoint**: Semantic HTML structure is complete. All states are represented.

### Phase 3: Apply Styling (Tokens Only)

1. Apply design tokens — NO hardcoded values:
   - Colors: `var(--color-primary-500)` or `text-primary-500` (Tailwind) or token references
   - Spacing: `var(--spacing-4)` or `p-4` (Tailwind) or token references
   - Typography: `var(--font-size-xl)` or `text-xl` (Tailwind) or token references
2. Style mobile-first:
   - Default styles = mobile
   - Add breakpoints for tablet and desktop enhancements
3. Implement all interactive states:
   - `:hover`, `:focus`, `:active`, `:disabled`
   - Focus rings or outlines for keyboard users
4. Use CSS Grid or Flexbox — avoid absolute positioning unless specifically required
5. Implement dark mode variants if project supports it

**Checkpoint**: UI is styled with tokens. Mobile-first is applied. All interactive states work.

### Phase 4: Implement Accessibility

1. Add ARIA attributes where needed:
   - `aria-label` for icon-only buttons
   - `aria-expanded` for expandable elements
   - `role="alert"` for dynamically appearing error messages
   - `aria-live` for content that updates dynamically
2. Ensure keyboard navigation:
   - Every interactive element is focusable
   - Tab order follows visual order
   - Modals trap focus and close with ESC
3. Add image alt text (descriptive for content images, empty for decorative)
4. Form inputs must have associated `<label>` elements
5. Add `autocomplete` attributes on form fields

**Checkpoint**: All accessibility attributes in place. Keyboard navigation works.

### Phase 5: Wire Up Data and Interactions

1. Connect real data sources (API calls, context, stores)
2. Implement loading states:
   - Show skeleton screens or spinners while loading
   - Never flash a loading state for < 200ms (avoids flicker)
3. Implement error states:
   - Show user-friendly error messages
   - Provide retry actions where appropriate
4. Implement empty states:
   - Show meaningful empty state with call-to-action
   - Never show a blank screen when data is empty
5. Wire up all interactions (clicks, form submissions, navigation)

**Checkpoint**: Full user flow works end to end. All states functional.

### Phase 6: Polish and Verify

1. Run through all states: Loading → Success, Loading → Error, Success → Empty
2. Test at minimum mobile width (375px), tablet (768px), desktop (1280px+)
3. Run accessibility audit (axe-core/Lighthouse) — zero violations
4. Check color contrast in both light and dark modes
5. Verify all interactive elements have visible focus states
6. Lint and format the code
7. Write or update component tests

**Checkpoint**: UI is production-ready. All checks pass.

## Quality Gates

- [ ] Semantic HTML used throughout
- [ ] Design tokens used — zero hardcoded values
- [ ] Mobile-first responsive design
- [ ] All states implemented (loading, empty, error, success)
- [ ] WCAG AA accessibility — zero violations
- [ ] Keyboard navigation works end to end
- [ ] Dark mode functional (if applicable)
- [ ] Components are reusable and composable
- [ ] Tests cover all states
- [ ] Lint passes with zero warnings

## Outputs

- Implemented, styled, accessible UI components
- Component tests
- Updated component library documentation (if new components created)

## Related Playbooks

- [UI Design](ui-design.md) — Creates the design specification used here
- [Design Review](design-review.md) — Review the implemented design
- [Build Feature](build-feature.md) — Broader feature implementation workflow
- [Code Review](code-review.md) — Required before merge

## Related Agents

- [Implementer](../agents/implementer.md) — Primary agent
- [Designer](../agents/designer.md) — Design review of the output
- [Reviewer](../agents/reviewer.md) — Code review
