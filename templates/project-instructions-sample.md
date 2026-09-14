# Project Instructions (sanitized sample)

> This is a genericized version of the standing-instructions file this workspace actually reads at the start of every session. The real one carries a name, real constraints, and real numbers; this one carries the *shape* of those rules so the mechanism is visible without the private content behind it.

---

## The one rule everything else depends on

**Nothing goes into an output that is not in the evidence file.**

No invented metrics, no assumed experience, no keyword that couldn't be defended under a follow-up question. If the evidence is thin, the answer is to say so and ask, not to fill the gap with something plausible. The whole system exists so that every claim survives a follow-up question well after the fact, where being caught costs far more than not having the answer in the first place.

---

## Files

| File | What it is |
|---|---|
| Evidence file | Source of truth. Every fact, background detail, and quotable number the agent is allowed to use, plus a companion list of facts that are true but cannot be safely quoted (stale, secondhand, or no longer verifiable), with the qualitative substitute to use instead. |
| Scoring rubric | The gated workflow — hard pass/fail gates, then a weighted score, then a verdict. Must be run and reported before any tailored output is produced. |
| Session memory | Append-only log of decisions, corrections, and open items, read at the start of every session. Version control shows what changed; this shows why. |
| Packaged skill | The repeatable pipeline for the actual output (in this case: research → keyword mapping → draft), run the same way every time instead of improvised per instance. |

---

## Workflow

**The gate runs first, always.** Given a new input, run the scoring rubric before producing anything else. Report the gate results and the score, then wait for a decision — do not proceed to output on inferred approval.

**Only then build the output.** If the gate passes, proceed through the packaged pipeline in order rather than skipping steps that feel obvious in the moment.

**Log the session.** At the end of any session that changed a decision, corrected a fact, or produced output, append an entry to the session memory. Record the reasoning, not just the outcome — and keep the open-items list honest. A stale "done" there is worse than no entry at all.

---

## Standing constraints

*(Placeholders below — the real file has actual values specific to one person's actual situation.)*

- **[Constraint A] is a gate, not a preference.** Confirm before investing in output; a term that sounds like it satisfies the constraint often doesn't survive a closer read.
- **[Constraint B] is a hard floor.** State it consistently; never negotiate downward from it in materials or conversation.
- **No [stylistic rule].** Consistency here is itself a signal of care.
- **Cap on parallel in-flight items.** Beyond a certain number, quality of attention collapses; better to do fewer well.

---

## Things that are easy to get wrong

This section exists because certain facts get restated incorrectly under time pressure unless they're written down explicitly, once, in a place every session re-reads. A few generic shapes this list actually takes:

- **A later-stage outcome gets misattributed as an upfront design choice**, when it was actually the result of a negotiation or a pivot partway through. State the sequence accurately; don't let hindsight flatten it into "planned from the start."
- **A strategy that was decided per-category gets misremembered as decided per-instance** (or vice versa). Precision here matters because it's exactly the kind of detail a technical follow-up question probes.
- **A number that was once obtainable is no longer obtainable.** Say so plainly rather than estimating a replacement.
- **A capability that sounds adjacent to one actually held gets claimed by association.** If the real experience is "we built an inheritance/cascade model," don't let it get restated as "we built role-based access control" just because they sound related.

---

## Open items

A living list of unresolved gaps, unanswered questions to ask a reference or a future interviewer, and pending cleanup — kept honest rather than aspirational, for the same reason the session log is.
