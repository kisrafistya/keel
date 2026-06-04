# Template: IMPLEMENTATION-PLAN

The build sequence: the governing strategy, the dependency-respecting tracks, the milestones, and an honest pre-build gap critique. Tier 2 and up.

## Questions it must answer

- What's the single governing strategy (the one rule that orders everything)?
- What are the parallel tracks, and what blocks what?
- What's the cross-module dependency map?
- What are the milestones, in order?
- What can start NOW vs what is blocked, and on what?
- What contradictions or gaps must be resolved BEFORE any code?

## Required sections

- `## The governing strategy` - the one sequencing principle (e.g. greenfield-first, risky-thing-last).
- `## Build sequence` - the tracks (A, B, C...), each with its start condition and what it depends on.
- `## Dependency map` - what sits on what; the concrete seam edges (consumer -> provider).
- `## Milestones` - M0..MN, each a verifiable state, not a vibe.
- `## Start NOW vs blocked` - two lists; for each blocked item, name the gate.
- `## Completeness critique` - the contradictions and gaps to resolve before code, ranked by severity.

## Good vs slop

Good: someone can pick up track A today knowing exactly what it depends on and what it unblocks. Slop: a flat to-do list with no dependencies, no gates, no "what blocks this" - which guarantees work in the wrong order.
