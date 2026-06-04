# Template: ARCHITECTURE & DECISIONS

The shape of the system and the decisions that gave it that shape. Reads as numbered decisions, each with its rationale, plus the invariants and the risk map. Tier 2 and up.

## Questions it must answer

- What are the core architectural decisions, and WHY each?
- What invariants must never break, and what happens if they do?
- What's the build sequence?
- Where are the risks, and how is each handled?
- What is the module / component layout?

## Required sections

- `## N. <decision>` - one numbered section per major architectural decision (e.g. platform/runtime, key/auth layer, data model, monetization model). Each states the decision and the reasoning, and cites the canonical DECISIONS doc where relevant.
- `## Invariants (break these and we lose it)` - the non-negotiable properties (security, custody, data integrity, correctness). State the consequence of breaking each.
- `## Build sequence` - the dependency-respecting order.
- `## Risk map` - each material risk, its failure mode, and the mitigation.
- `## Module layout` - the components, and what each one owns.

## Good vs slop

Good: every decision carries its reason, and the invariants section names the consequence of violating each. Slop: a box-and-arrow diagram with no rationale and no invariants - which is exactly how the model later "improves" something load-bearing without knowing it was load-bearing.
