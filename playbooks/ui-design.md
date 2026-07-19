---
id: PLBOOK-009
title: UI Design
version: 1.0.0
status: active
agent: designer
triggers:
  - "design"
  - "UI"
  - "UX"
  - "component design"
  - "interface"
  - "layout"
  - "style"
  - "visual"
  - "look and feel"
---

# UI Design

> Design user interfaces from concept to component specification, ensuring visual quality, consistency, and accessibility.

## Prerequisites

- [ ] Design tokens are defined (colors, typography, spacing)
- [ ] Design principles are documented for the project
- [ ] Component library is referenced (shadcn/ui, Tailwind UI, MUI, custom, etc.)
- [ ] User flow or feature spec exists

## Workflow

### Phase 1: Understand the User

1. Read the feature spec or user story
2. Map the user flow: what does the user do, step by step?
3. Identify all states for every interactive element:
   - Default / Resting
   - Hover
   - Focus (keyboard)
   - Active / Pressed
   - Disabled
   - Loading
   - Empty (no data)
   - Error
   - Success
4. Identify edge cases: long text, no data, error states, first-time user, returning user

**Checkpoint**: You understand the full user journey and all states.

### Phase 2: Component Architecture

1. Break the UI into a component tree (atomic design: atoms → molecules → organisms → templates)
2. For each component, define:
   - Props / API surface
   - States it must handle
   - Accessibility requirements
   - Responsive behavior (mobile → tablet → desktop)
3. Reuse existing components from the component library whenever possible
4. Only create new components when no existing component fits

**Checkpoint**: Component tree is mapped. Every component has a clear specification.

### Phase 3: Visual Design

Applying the project's design tokens:

1. **Layout**: Define the spatial structure
   - Grid system, spacing between elements
   - Mobile-first: design for 375px width first, then enhance
   - Use spacing tokens (e.g., `spacing-4` not `16px`)
2. **Typography**: Define text hierarchy
   - Heading levels (h1, h2, h3, h4)
   - Body text, captions, labels
   - Use typography tokens (e.g., `text-xl` not `20px`)
3. **Color**: Apply color tokens
   - Primary, secondary, neutral, semantic (success, warning, error)
   - Ensure sufficient contrast (4.5:1 normal, 3:1 large)
   - Dark mode: define dark mode variants for all colors
4. **Interactive Elements**: Buttons, inputs, links
   - Consistent sizing (use spacing tokens)
   - Clear affordance (what's clickable looks clickable)
   - Focus rings for keyboard navigation
5. **Motion**: Define transitions and animations
   - Prefer subtle, purposeful animations
   - Respect `prefers-reduced-motion`

**Checkpoint**: Visual design is complete, token-based, and covers all states.

### Phase 4: Accessibility Check

Verify WCAG AA compliance:

1. Color contrast: all text meets minimum contrast ratios
2. Keyboard: all interactive elements are reachable and operable via keyboard
3. Screen reader: meaningful alt text, ARIA labels where needed
4. Focus management: focus order is logical, focus is visible
5. Forms: all inputs have labels, error messages are descriptive

**Checkpoint**: UI meets WCAG AA standards.

### Phase 5: Deliver

For AI-to-code workflows, deliver the design as:

1. **Component specification**: Component name, props, states, accessibility notes
2. **Layout description**: How components compose together
3. **Token references**: Which design tokens to use (not hardcoded values)
4. **State matrix**: Loading / Empty / Error / Success for every data-dependent component
5. **Responsive breakpoints**: How the layout changes at each breakpoint

```
Example: "LoginForm component
- Props: onSubmit(email, password), isLoading, errorMessage
- States: default, loading (button shows spinner), error (inline error message), success (redirect)
- Accessibility: email input has autocomplete='email', password has autocomplete='current-password', error message has role='alert'
- Responsive: full-width on mobile, max-w-md centered on desktop
- Tokens: background: neutral-50, input border: neutral-300, button: primary-600, error text: semantic-error"
```

**Checkpoint**: Design is delivered as an implementable specification, not just a visual description.

## Quality Gates

- [ ] All states designed (loading, empty, error, success, edge cases)
- [ ] Component tree is defined
- [ ] Design tokens used (no hardcoded values)
- [ ] Mobile-first responsive design
- [ ] Accessibility verified (WCAG AA)
- [ ] Dark mode considered (if project supports it)
- [ ] Existing components reused where possible

## Outputs

- Component specification (component tree + props + states)
- State matrix (for all data-dependent components)
- Responsive layout description
- Token references (which tokens to use where)

## Related Playbooks

- [Design Review](design-review.md) — Review the design before implementation
- [Design-to-Code](design-to-code.md) — Convert this design into code
- [Build Feature](build-feature.md) — Implement the designed feature

## Related Agents

- [Designer](../agents/designer.md) — Primary agent
- [Implementer](../agents/implementer.md) — Implements the design
