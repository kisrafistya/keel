---
name: keel
description: "Process and judgment skill for AI-assisted building - the anti-slop method that runs before and around the code. Use when starting a new idea or project, when someone asks how we work or how to vibecode without slop, when you need to pressure-test an idea, scaffold the right docs, lock decisions, or gate a build on readiness. The upstream companion to a design skill: keel decides WHAT to build and whether it holds; the design skill makes the UI look made, not generated."
version: 1.0.0
---

# Keel

A process skill for AI-assisted building. It makes sure you build the right thing, with conviction, before and while you vibecode - so the work is considered, not slop.

Lay the keel first. The keel is the spine a ship is built around; without it the rest capsizes. This skill is the spine of a project: the thinking, the locked decisions, and the discipline that everything else hangs off.

**The differentiator.** Code generation is solved. An AI will happily build whatever you point it at, fast and confidently. So the failure mode is no longer "can't build it" - it's **building the wrong thing faster, on no foundation, with the model amplifying every unexamined assumption.** Keel front-loads the part that is still hard: find the real insight, pressure-test it honestly, lock the decisions so the model can't drift, document just enough, and gate the build on readiness. Vibecoding without this produces slop that compiles.

This skill is general. It is not tied to any one product, stack, or domain. It scales down to a weekend script and up to a funded company.

---

## How to use this skill

Keel has one default behaviour and a few explicit verbs.

| Invocation | What it does |
| --- | --- |
| *(default)* / `keel start` | A new idea or project. Run the **Groundwork flow**: find the insight, pressure-test it, lock decisions, right-size the docs, gate the build. |
| `keel task <description>` | A coding task on an existing project. Run the **Work loop**: orient, plan, act, verify, checkpoint. Anti-slop discipline, never self-merge. |
| `keel pressure-test <idea or claim>` | Run only the idea-vs-insight stress test. Load [`references/pressure-test.md`](references/pressure-test.md) and follow it. |
| `keel docs` | Scaffold or right-size the document set for the project's tier. Load [`references/scaffold.md`](references/scaffold.md), then load only the `references/doc-*.md` templates for the chosen set. |
| `keel review <target>` | Build-readiness / gap audit before shipping or before building further. Load [`references/doc-build-readiness.md`](references/doc-build-readiness.md) and produce the scorecard. |

If the input doesn't map to a verb, treat it as default.

**References load on demand, not up front.** Read a `references/` file only when the step that needs it runs. The doc templates each carry the required section skeleton, the questions that doc must answer, and a "good vs slop" line - load only the ones for the tier you're scaffolding. The full index is at the end of this file.

---

## Operating principles (always on, every verb)

These are not steps. They hold the whole time.

1. **Think before coding.** State assumptions out loud. If something is ambiguous, ask instead of guessing. If a simpler approach exists, say so. If you are confused, stop and name what is unclear.
2. **Simplicity first.** The minimum that solves the problem. Nothing speculative. No abstraction for single-use code.
3. **Surgical changes.** Touch only what the task needs. Match the existing style. Don't "improve" adjacent code.
4. **Read before you write.** Read the canon, the exports, the immediate callers, the shared utilities, before adding anything. "Looks orthogonal" is where bugs hide.
5. **Goal-driven.** Define success criteria, then loop until verified. Don't just run steps.
6. **Surface conflicts, don't average them.** If two patterns contradict, pick one (more recent / more tested), say why, flag the other. Never blend.
7. **Checkpoint after each significant step.** Summarize what's done, what's verified, what's left. Don't continue from a state you can't describe.
8. **Tests verify intent, not just behaviour.** A test must encode *why* the behaviour matters. A test that can't fail when the business logic changes is wrong.
9. **Fail loud.** "Done" is wrong if anything was skipped silently. "Tests pass" is wrong if any were skipped. Default to surfacing uncertainty.
10. **Use the model for judgment, not for plumbing.** Classify, draft, summarize, extract - yes. Routing, retries, deterministic transforms - no. If code can answer, code answers.

---

## Disciplines that hold across every verb

Four disciplines that are not specific to any one flow. They are the anti-slop core.

1. **Honest content - no fabricated premises.** Never invent a number, metric, fact, or user the brief didn't supply. Supply structure and arithmetic; the human supplies the empirical premises. When a value is assumed, mark it as an assumption and say what must be confirmed. An invented "+40% faster" or a guessed volume figure is slop the moment it's typed.

2. **Verify before you quote.** Any third-party fact - an API field's meaning, a token's decimals, a claimed statistic, the authenticity of an email - gets checked against the source before you rely on it. Restating someone's claim as verified fact is how wrong numbers propagate through four documents.

3. **Lock decisions, never silently re-decide.** Once a choice is settled, write it to a canonical decisions document with the reason. New work reads that document first. The number-one failure mode of long AI sessions is the model quietly contradicting an earlier decision; a locked-decisions file is the fix. Re-opening a locked decision requires explicit cause, stated.

4. **Get an independent perspective before committing.** On non-trivial work, pull a second, stronger review before you commit to an approach and again before you declare done. A passing self-test is not evidence your approach is right - it's evidence your test agrees with you.

---

## The Groundwork flow (default - a new idea or project)

### 0. Orient

Read whatever already exists - canon docs, prior decisions, existing code - **before proposing anything.** Orientation is not "substantive work"; skipping it is.

### 1. Find the insight, not just the idea

- The **idea** is the consensus version: what anyone would say the thing is. ("An embedded wallet SDK." "A todo app with AI.") If that's all there is, well-resourced players are already there, and you're late.
- The **insight** is the non-consensus belief underneath, usually born of lived experience: the thing you believe that the market prices wrong. Name it in one sentence. If you can only find the idea and not the insight, **say so plainly** - that's a finding, not a failure.

### 2. Pressure-test the insight (the real test, not consensus-grading)

**Load [`references/pressure-test.md`](references/pressure-test.md) and follow it.** In summary: this is where most "validation" goes wrong. An adversarial pass that grades a non-consensus insight against consensus will always kill it - because from the outside, a real insight is indistinguishable from being wrong. Run the honest test instead:

- **Why now** - what changed that makes this possible/urgent today and not three years ago.
- **Why you** - the unfair, hard-to-replicate edge. Be specific.
- **Why different** - and test it against the **best-positioned incumbent**, not the current market. "Why won't the giant who already has the distribution just do this?"
- **The leap-of-faith assumption** - state the one or two beliefs the whole thing rests on, crisply.
- **What would break each** - for every load-bearing assumption, name the cheap, falsifiable test that would prove it *wrong*. "What would make me wrong" is the test, not "what confirms me."

Don't kill a non-consensus insight by grading it against consensus. Don't bless a consensus idea as an insight either. Both errors are slop.

### 3. Lock the decisions

Capture every choice that is now settled into a canonical decisions document: the decision, the date, the reason, and a "locked" marker. These are the things downstream work must not re-litigate. This is what keeps the model (and the team) from drifting.

### 4. Right-size the docs

Generate only the documents this project's tier warrants (see **The doc taxonomy** below). A weekend tool does not get thirty documents. Ceremony beyond the project's seriousness is itself a form of slop.

**Load [`references/scaffold.md`](references/scaffold.md)** for the interview and the tier-to-doc-set map, then load **only** the `references/doc-*.md` templates for the chosen set. Emit each doc as its section skeleton with a one-line prompt under every header - never invented content.

### 5. Build-readiness gate

Before building, audit the gaps honestly. For each area, mark it **decided / designed / unknown / not-covered**. Surface the not-covered items loudly. Don't declare "ready to build" when the honest state is "ready to build three of seven pieces." Fail loud here and you save a rewrite later.

---

## The Work loop (`keel task` - an existing project)

For any non-trivial coding task:

**orient** (read the canon plus the exact code you'll touch) -> **plan** (state the approach and the success criteria; get a second perspective if it's non-trivial) -> **act** (surgical, match conventions) -> **verify** (against the success criteria; tests encode intent) -> **checkpoint** (summarize done / verified / left).

Never self-merge or ship without review. Fail loud if any step was skipped.

---

## The doc taxonomy (right-sized, general)

Three tiers. Pick the smallest that fits. Every doc does **one** job and points to the owner of anything it references (don't duplicate - duplicated docs drift).

**Tier 1 - Weekend** (a script, a tool, a throwaway):
- `README` - what it is, why, how to run it.
- `DECISIONS` - the handful of choices you locked.
- That's the whole set. Resist more.

**Tier 2 - Serious** (a product you intend to maintain):
- `README`, `DECISIONS` (canonical, locked).
- `POSITIONING` - who it's for and the wedge.
- `ARCHITECTURE` - the shape, the data model, and the invariants that must never break.
- One design doc **per non-trivial subsystem**.
- `IMPLEMENTATION-PLAN` - the build sequence and the critical path.
- `ENGINEERING-STANDARDS` - the conventions the code (and the AI) must follow.

**Tier 3 - Fundable** (capital, a team, users, maybe regulation):
- Everything in Tier 2, plus:
- `MESSAGING` - the words, and what *not* to say.
- `PRICING`, `CRITICAL-PATH`, `BUILD-READINESS`.
- `GTM`, `RUNWAY-AND-FUNDRAISE`.
- Whatever legal / compliance / ops / runbook docs the domain actually requires - and no more.

Tier up when the stakes rise, not before.

---

## Anti-slop tells (the process equivalents of UI slop)

If you catch any of these, stop and fix the process, not just the artifact:

- Building before the insight is named.
- Re-deciding a settled question mid-session (drift).
- Inventing a number, metric, or fact to fill a gap in a doc.
- Two docs covering the same thing with no single owner.
- "Done" claimed with steps silently skipped.
- Thirty documents for a weekend project (ceremony over substance).
- Averaging two conflicting patterns instead of picking one and flagging the other.
- Quoting a third-party fact you never verified.

---

## References

Load on demand, only when the step that needs it runs.

**Process:**
- [`references/scaffold.md`](references/scaffold.md) - the interview + tier-to-doc-set map (Groundwork step 4, `keel docs`).
- [`references/pressure-test.md`](references/pressure-test.md) - the full idea-vs-insight framework + output format (Groundwork step 2, `keel pressure-test`).

**Doc templates** (each: required sections + the questions it must answer + good-vs-slop):
- Tier 1+: [`doc-readme.md`](references/doc-readme.md), [`doc-decisions.md`](references/doc-decisions.md)
- Tier 2+: [`doc-positioning.md`](references/doc-positioning.md), [`doc-architecture.md`](references/doc-architecture.md), [`doc-design-module.md`](references/doc-design-module.md), [`doc-implementation-plan.md`](references/doc-implementation-plan.md), [`doc-engineering-standards.md`](references/doc-engineering-standards.md)
- Tier 3: [`doc-messaging.md`](references/doc-messaging.md), [`doc-pricing.md`](references/doc-pricing.md), [`doc-critical-path.md`](references/doc-critical-path.md), [`doc-build-readiness.md`](references/doc-build-readiness.md), [`doc-gtm.md`](references/doc-gtm.md), [`doc-runway.md`](references/doc-runway.md)

**Worked examples** (filled docs for a sample project, as imitation targets - read one when a skeleton alone isn't enough):
- [`examples/EXAMPLE-decisions.md`](references/examples/EXAMPLE-decisions.md), [`examples/EXAMPLE-design-module.md`](references/examples/EXAMPLE-design-module.md)

## Handoff

When the groundwork holds and you reach the actual UI build, hand off to the design skill (e.g. **Hallmark**) for the visual layer. Keel decides *what* to build and whether it holds up; the design skill makes sure it looks made, not generated. Together they cover both halves of anti-slop: the thinking and the surface.
