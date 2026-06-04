# Template: ENGINEERING-STANDARDS (governs all production code)

The conventions the code - and the AI writing it - must follow. Enforced, not decorative. Tier 2 and up.

## Questions it must answer

- What are the few principles every file obeys?
- What are the hard, reviewable rules (size, structure, language policy, efficiency)?
- What's the enforcement: rule -> tool -> gate?
- Where do these apply (code vs docs vs scripts)?

## Required sections

- `## The principles (enforced, not decorative)` - the two to four rules that override personal taste.
- `## Hard rules` - concrete, reviewable limits (e.g. a file-size cap, one-language-per-layer, named efficiency rules). Each must be checkable, not aspirational.
- `## Enforcement matrix` - a table: rule -> the tool that catches it -> the gate (lint / CI / review) that blocks it.
- `## Scope` - what these govern, and what they don't.

## Good vs slop

Good: every rule has a tool or a gate that enforces it, so it's real. Slop: "write clean code, prefer readability" - unenforceable vibes the AI will quietly ignore under pressure.
