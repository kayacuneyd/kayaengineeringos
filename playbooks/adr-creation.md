---
id: PLBOOK-006
title: ADR Creation
version: 1.0.0
status: active
agent: architect
triggers:
  - "ADR"
  - "architecture decision"
  - "decision record"
  - "architectural decision"
  - "create ADR"
---

# ADR Creation

> Create an Architecture Decision Record to document significant technical decisions with context, options, and consequences.

## Prerequisites

- [ ] A significant architectural decision needs to be made or has been made
- [ ] At least two viable options have been identified
- [ ] Key stakeholders are available for discussion (if team project)

## When to Create an ADR

Create an ADR when:

- Choosing a technology, framework, or library for the project
- Selecting an architectural pattern (MVC, microservices, monorepo, etc.)
- Defining a new convention that affects the whole project
- Changing an existing architectural decision
- Deprecating a previously used approach
- Deciding on data storage strategy
- Defining API design patterns
- Setting deployment or infrastructure strategy

Do NOT create an ADR for:

- Routine implementation details
- Decisions that can be easily reversed
- Obvious choices with no real alternatives

## Workflow

### Phase 1: Identify the Decision

1. Clearly state the problem or need
2. Document the forces at play:
   - Technical constraints
   - Business requirements
   - Team capabilities and preferences
   - Timeline and resource constraints
   - Existing patterns in the codebase
3. Define what a good decision looks like

**Checkpoint**: The problem is clearly stated and forces are documented.

### Phase 2: Evaluate Options

1. List at least 2 viable options (more is fine, less is not enough)
2. For each option:
   - What are the pros?
   - What are the cons?
   - What are the trade-offs?
   - What would implementation look like?
3. Research: are there ADRs from other projects? Prior art?
4. Prototype if the decision is high-risk

**Checkpoint**: All viable options are evaluated with pros, cons, and trade-offs.

### Phase 3: Decide

1. Select the option that best addresses the forces at play
2. Clearly document WHY this option was selected over others
3. Document WHY each rejected option was rejected
4. Be honest about the negatives of the chosen option — no perfect solutions

**Checkpoint**: Decision is made and rationale is documented.

### Phase 4: Write the ADR

1. Use the ADR template (`adr/_template.md`)
2. Assign the next sequential number (check `adr/INDEX.md`)
3. Fill in all sections:
   - Context: what problem, what forces
   - Decision: what we chose and why
   - Options Considered: what else we looked at
   - Consequences: what gets easier, what gets harder
4. Mark status as `accepted`
5. Add references to related ADRs, documentation, discussions

**Checkpoint**: ADR is complete and follows the template.

### Phase 5: Register and Share

1. Add the ADR to `adr/INDEX.md`
2. Update the Qucik Reference section if a new topic is introduced
3. If superseding a previous ADR:
   - Update the old ADR's status to `superseded`
   - Add `superseded_by` to the old ADR
   - Add `supersedes` to the new ADR
   - Update the Supersession Chain in INDEX.md
4. Share the ADR with the team for awareness

**Checkpoint**: ADR is registered, indexed, and visible.

## Quality Gates

- [ ] Problem is clearly stated
- [ ] At least 2 viable options evaluated
- [ ] Decision is justified with clear rationale
- [ ] Consequences (good and bad) are documented
- [ ] ADR follows the template format
- [ ] ADR is registered in INDEX.md
- [ ] Supersession chain is maintained (if applicable)

## Outputs

- New ADR file in `adr/NNNN-title.md`
- Updated `adr/INDEX.md`
- Updated superseded ADR (if applicable)

## Related Playbooks

- [Build Feature](build-feature.md) — ADRs inform implementation
- [Code Review](code-review.md) — Reviewers check ADR compliance

## Related Agents

- [Architect](../agents/architect.md) — Primary agent
- [Implementer](../agents/implementer.md) — Implements decisions
- [Reviewer](../agents/reviewer.md) — Verifies ADR compliance
