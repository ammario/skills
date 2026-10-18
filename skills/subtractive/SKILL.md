---
name: subtractive
description: >-
  Deliver features subtractively: net-reduce complexity and production LoC in
  the area under development, or pay for unavoidable additions by simplifying
  elsewhere. Use when the user asks to work subtractively or simplify.
disable-model-invocation: true
---

# Subtractive

Ship the feature while leaving the codebase net simpler. Assess complexity
in both **LoC** (implementation volume) and **concepts** (state, branching,
coupling, mechanisms, and abstractions). Fewer lines alone do not prove
simplification; report the conceptual change as well.

The reduction budget is net production LoC. Tests and docs do not spend that
budget, but they are not invisible: include them and all other changes in
the ledger. Relocating complexity into tests, config, or generated code is
laundering, not reduction.

1. **P1 — Simplify the area under development.** Conceptual complexity and
   net production LoC in the touched area go down. Subtract first: reshape
   the area until the feature drops in cleanly, then make the now-easy
   change. Ask what the
   feature obsoletes — special cases, config knobs, dual paths, abstractions
   that worked around the problem now being solved properly.
2. **P2 — Pay elsewhere.** Only if P1 is impossible or would damage
   maintainability, offset the addition by simplifying other code in the
   same change, preferring the same module or crate.

The largest subtractions happen at design time: prefer the mechanism-poor
design — derive state rather than store and synchronize it, enforce an
invariant rather than handle its violations, lift a restriction rather than
build machinery around it. Interrogate the requirement itself: a smaller
feature surface often satisfies the actual need.

Reduction sources: dead code and stale gates; duplicate logic and parallel
string/enum mappings; single-caller or single-impl abstractions; defensive
handling of impossible states; speculative generality; forwarding-only
wrappers; comments narrating what the code already says.

Rules:

- Readability outranks line count; a clear +10 beats an opaque -5.
- Verify deletions are safe: callers, log contracts, programmatic consumers,
  tests. Never delete a critical safety check to fund a feature.
- Offsets that belong in their own commit get their own commit.
- Subtraction is not churn: leave untouched what is merely imperfect.

## Report

End with a report containing the change ledger, an index of observed
complexity, and changes the user could make to enable further simplification.

### Ledger

Cover both dimensions:

- **LoC:** added, removed, and net lines for production code, tests,
  docs/comments, configuration/build files, generated artifacts, and other
  changes as applicable, plus a whole-change total. State the counting
  convention; count each changed line once and do not omit non-production
  growth just because it is outside the reduction budget.
- **Concepts:** what was added, removed, or simplified — e.g. state owners,
  gates, knobs, dual paths, abstractions, and coupling. Explain why the net
  design is simpler, including any trade-off between LoC and concepts.
- **Safety:** why the subtractions were safe and how they were verified;
  if P2 was necessary, explain why in-place reduction was not viable.

### Observed complexity

Index the complexity observed during the work, with code locations and a
brief explanation of each item. Distinguish:

- **Addressed:** what this change removed or simplified, referring to the
  ledger where useful.
- **Irreducible:** what remains necessary under the current requirements
  and constraints, and why it cannot be simplified further.
- **Future work:** remaining candidates for simplification, the likely
  approach or next investigation, and why they were deferred.

Keep the index scoped to what was actually examined. State uncertainty
where more investigation is needed; deferral alone does not establish
irreducibility. Reporting a candidate does not expand the current task.

### User choices that enable further simplification

Actively look for complexity sustained by the user's behavior, workflow,
requirements, or operating practices. Surface concrete changes the user
could make to remove that complexity, including changes to constraints
that make an item currently irreducible. For each opportunity, explain the
user action or decision, the code or concepts it would eliminate, and the
resulting trade-off in capability, convenience, or operational burden.
Prioritize the opportunities with the greatest simplification benefit;
do not invent recommendations when none are supported by the work.

Present these as choices for the user. Do not silently change requirements
or count shifting complexity into manual work as eliminating it.
