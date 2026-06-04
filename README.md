# Keel

**The anti-slop layer for AI-assisted building.** Keel is the process and judgment that runs *before and around* the code, so you build the right thing instead of generating slop that compiles.

It works two ways: as a [Claude Code](https://claude.com/claude-code) / agent skill you can drop in, and as a plain method you can just read.

---

## Why

Code generation is solved. An AI will happily build whatever you point it at, fast and confidently. So the failure mode is no longer "can't build it" - it is **building the wrong thing faster, on no foundation, with the model amplifying every unexamined assumption.**

Keel front-loads the part that is still hard:

- **Find the real insight**, not just the consensus idea.
- **Pressure-test it honestly**, without consensus-grading a non-consensus bet to death.
- **Lock the decisions** so the model can't quietly drift or contradict itself mid-session.
- **Right-size the docs** - a weekend script does not get thirty documents.
- **Gate the build on readiness** instead of vibing straight into production.

## What's inside

- **Operating principles** plus four **anti-slop disciplines**: honest content (no fabricated numbers), verify-before-quoting, lock-decisions, and second-perspective-before-committing.
- **The Groundwork flow** for a new idea: orient -> find the insight -> pressure-test -> lock decisions -> right-size docs -> build-readiness gate.
- **The Work loop** for everyday tasks: orient -> plan -> act -> verify -> checkpoint.
- **A tiered doc taxonomy** (Weekend / Serious / Fundable) with **13 doc templates**, each carrying its required sections, the questions it must answer, and a good-vs-slop line.
- **A pressure-test framework** - the idea-vs-insight test: why-now / why-you / why-different / what-would-break-it.
- **Worked examples** of filled docs as imitation targets.

## Use it as a skill

Clone it into your agent's skills directory:

```bash
# Claude Code (global)
git clone https://github.com/kisrafistya/keel ~/.claude/skills/keel

# or into a single project (.claude/skills/ or .agents/skills/)
git clone https://github.com/kisrafistya/keel .claude/skills/keel
```

Then invoke it:

| Command | What it does |
| --- | --- |
| `keel start` | New idea: find the insight, pressure-test, lock decisions, scaffold docs, gate the build. |
| `keel task <desc>` | A coding task: orient -> plan -> act -> verify -> checkpoint. |
| `keel pressure-test <idea>` | Run the idea-vs-insight stress test on its own. |
| `keel docs` | Scaffold the right-sized doc set for your tier. |
| `keel review <target>` | Build-readiness / gap audit. |

The skill also auto-triggers when you ask things like "how do I start this project," "pressure-test this idea," or "what docs do I need," so you don't have to memorize the verbs.

## Use it as a method (no tools required)

Just read [`SKILL.md`](SKILL.md). It is the whole method in one file, with the [`references/`](references/) directory holding the templates and worked examples. None of it is Claude-specific: the principles, the flow, and the doc shapes apply to any AI coding assistant, or to no AI at all.

## The doc tiers

- **Weekend** (a script, a throwaway): `README` + `DECISIONS`. Stop there.
- **Serious** (a product you'll maintain): adds `POSITIONING`, `ARCHITECTURE`, per-subsystem design docs, `IMPLEMENTATION-PLAN`, `ENGINEERING-STANDARDS`.
- **Fundable** (capital, team, users, regulation): adds `MESSAGING`, `PRICING`, `CRITICAL-PATH`, `BUILD-READINESS`, `GTM`, `RUNWAY`, and whatever your domain requires.

Tier up when the stakes rise, not before.

## Why "keel"

The keel is the spine a ship is built around; without it, the rest capsizes. This is the spine of a project: the thinking and the locked decisions that everything else hangs off.

## Companion

Keel decides *what* to build and whether it holds up. For the UI layer - making what you build look made, not generated - pair it with a design skill.

## Contributing

Issues and PRs welcome: new doc templates, sharper good-vs-slop lines, more worked examples, or tuning the flows. Keep additions general and tool-agnostic.

## License

[MIT](LICENSE). Built by [@kisrafistya](https://github.com/kisrafistya).
