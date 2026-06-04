# Template: design module (one per non-trivial subsystem)

The contract for a single subsystem. Prose and shapes, not code. One file per subsystem; it owns that subsystem's truth and other docs point to it (DRY). Tier 2 and up.

## Questions it must answer

- What is this subsystem's purpose and exact scope, and what is out of scope?
- What is the model - how does it actually work?
- What is the public interface / contract surface (shapes, not code)?
- What invariants must it hold?
- What does it depend on, and what depends on it?
- What are the risks and edge cases?
- What is the phased implementation plan?

## Required sections

- `## 1. Purpose & scope` - including explicit non-goals.
- `## 2. The model` - the core mechanic, stated plainly.
- `## 3. Core mechanics` - the main flows.
- `## 4. Public interface / contract surface` - the shapes that cross the boundary, in prose. No code.
- `## 5. Invariants` - what must always hold.
- `## 6. Dependencies` - consumers and providers, the concrete seam edges (what crosses, in which direction).
- `## 7. Risks & edge cases`.
- `## 8. Phased implementation plan` - P0..PN.
- `## 9. Sources` - anything external the design rests on.

## Good vs slop

Good: another engineer (or the AI) can build against the contract without reading the implementation. Slop: pasted code, or a description so vague the seam is ambiguous and two modules implement it differently.
