# Template: BUILD-READINESS

The honest scorecard: are we ready to build, and - separately - ready to launch? Grades each dimension and surfaces what is NOT covered. Tier 3, and the doc `keel review` produces.

## Questions it must answer

- Ready to START BUILDING? (Often a qualified yes.)
- Ready to LAUNCH / go live with real stakes? (Often a clear no - say so.)
- Per dimension, what's the state: decided / designed-not-built / unknown / not-covered?
- What did this pass change, and what did it deliberately NOT change?
- What's the single highest-leverage external gate?

## Required sections

- `## The two questions (the verdict)` - (A) ready to build? (B) ready to launch? Answer each plainly, up top.
- `## The legend` - define the grades: **decided / designed-not-built / unknown / not-covered**.
- `## Scorecard by dimension` - a row per dimension (architecture, security, legal, ops, GTM, ...), each graded.
- `## What this pass changed` - the gap-closure index.
- `## What this pass did NOT change` - the items that are founder / counsel / execution, not design.
- `## The highest-leverage external gate` - the one thing that most blocks launch.
- `## Next move`.

## Good vs slop

Good: it separates "ready to build" from "ready to launch," and refuses to mark a not-covered item as done. Slop: a green-light dashboard that hides the not-covered rows. Fail loud here - this is the doc whose whole value is honesty.
