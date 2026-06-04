# Template: DECISIONS (canonical, governs everything)

The anti-drift spine. Every settled choice lives here with its reason. New work reads this **first**. The model and the team must not silently re-decide anything locked here. Tier 1 and up.

## Questions it must answer

- What is in scope, and what is explicitly NOT (the product boundary)?
- What decisions are locked, and why?
- What was open and is now resolved?
- What is still tracked but not yet decided?
- What invariants must hold across all work?

## Required sections

- `## Product boundary (read first)` - what this is and is not, in one paragraph.
- `## Locked` - the decisions. Number them so other docs can cite "decision #N."
- `## Resolved` - things that were open and got closed, with how.
- `## Still tracked` - open questions, ranked, each with what unblocks it.
- `## Invariants` - the rules no module may break.

## Entry format (use verbatim)

`#N. <decision>. (locked <date>) - <reason>. <optional: supersedes #M / see also #K>.`

## Good vs slop

Good: you hand this to a new person and they will not reopen a settled debate, because each decision carries its date and reason. Slop: vague principles with no dates, no reasons, and no way to tell what's locked from what's still soft. A decisions doc that doesn't stop re-litigation isn't doing its one job.
