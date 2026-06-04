# Scaffold: interview first, then emit the right doc set

Run this at the top of the Groundwork flow, before writing any doc. The goal is to emit only the documents the project's stakes warrant, each pre-filled with the right section skeleton and a one-line prompt under every header - never invented content.

## The interview (ask once, bundled)

Ask these together. If the user waves you through, infer from context and state the inferences back in one line.

1. **What is it** - one sentence.
2. **Stakes / tier** - a throwaway/weekend thing, a product you'll maintain, or something fundable (capital, team, users, maybe regulation)?
3. **Domain** - consumer / B2B / infra / regulated? Anything that imposes legal, compliance, or money-handling constraints?
4. **Who's building** - solo, or a team that needs shared conventions?
5. **External gate** - any licence, partner, or capital dependency the build waits on?

## Tier -> doc set

- **Tier 1 (Weekend):** `doc-readme`, `doc-decisions`. Stop there.
- **Tier 2 (Serious):** `doc-readme`, `doc-decisions`, `doc-positioning`, `doc-architecture`, one `doc-design-module` per non-trivial subsystem, `doc-implementation-plan`, `doc-engineering-standards`.
- **Tier 3 (Fundable):** everything in Tier 2, plus `doc-messaging`, `doc-pricing`, `doc-critical-path`, `doc-build-readiness`, `doc-gtm`, `doc-runway`, and the domain's required legal / compliance / ops docs (and no more).

Load only the `doc-*.md` templates for the chosen set.

## Rules

- **Tier up when stakes rise, not before.** Over-documenting a small thing is itself slop.
- **One job per doc.** If two docs cover the same ground, one points to the owner (DRY).
- **Lock decisions as you make them** in `doc-decisions`, so nothing downstream re-litigates.
- **Emit skeletons, not content.** Each section gets its header plus a prompt for what goes there. You fill content only from what the user actually supplies (see the honest-content discipline in SKILL.md).
