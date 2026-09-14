# Architecture

Four components, each solving a specific failure mode I anticipated (or hit) while using an agent for real, consequential output.

## 1. A gate before expensive output

Tailoring a resume and researching a company properly takes real time. Most of that time is wasted if the role was never a fit to begin with. So the workflow is split in two, with a hard stop in between:

1. **Stage 0 — pass/fail gates.** A handful of non-negotiable conditions (location eligibility, compensation floor, whether the posting is even still live) get checked first. Any fail, or any gate the agent can't confirm from the source material, ends the workflow right there — it does not fall through to scoring.
2. **Stage 1 — weighted score.** Only if every gate passes does the agent score the role against weighted criteria and produce a verdict.

The agent has to *report* the gate results and the score and then **wait**. It does not proceed to writing a resume on its own judgment. This is the same instinct as a staged rollout or a feature flag: put the checkpoint where a wrong call is expensive, not where it's convenient to code.

See [`templates/fit-check-rubric-template.md`](../templates/fit-check-rubric-template.md) for the actual rubric shape (values genericized).

## 2. Grounding over prompting

The naive fix for "the model sometimes makes things up" is a better system prompt: "only state true things," "be accurate." That doesn't hold up under pressure — the model doesn't know what it doesn't know, and a sufficiently specific-sounding JD requirement will pull a plausible-but-invented answer out of it anyway.

The actual fix was structural, not verbal:

- **One evidence file** is the only source any claim can come from. Not "recent context," not "what sounds right for this JD" — one file.
- **A parallel do-not-quote list** for numbers or claims that are *technically true but not safely quotable* (a stale figure, a number obtained secondhand, a metric that's since become unverifiable). This is a different failure mode from "false" — it's "true once, now unconfirmable" — and it needed its own list rather than being lumped in with fabrication.
- **An explicit cannot-evidence table** for JD terms with no backing at all. If a job description asks for a keyword I can't defend, it goes in that table, not onto the page with a softened synonym. Getting a resume *through* an applicant-tracking system with an indefensible keyword is worse than not matching it, because it just moves the failure point to the interview, where it's more expensive.

See [`docs/grounding-example.md`](grounding-example.md) for what this looks like catching a real near-miss.

## 3. Memory designed for the next session, not this one

Two different kinds of history need to persist across a project like this, and they don't belong in the same place:

- **What changed** — git already does this well. A diff is a diff.
- **Why it changed, and what's still unresolved** — this is the part that evaporates if it isn't written down deliberately. An append-only run log, read at the start of every session, carries the reasoning: which decision was made, why, what got corrected, and — critically — an honest open-items list. A stale "done" in that log is worse than no entry at all, because it stops a future session from re-checking something that actually still needs work.

## 4. Iterating from observed failures, not hypothetical ones

Every fix to the standing rules in this workspace traces back to a specific, dated failure, not a "this could theoretically go wrong" guess. Four of them, generalized, are in [`docs/iteration-log.md`](iteration-log.md). The pattern in all four is the same: something slipped through once, the root cause got named precisely, and the fix became a rule inherited by every future session automatically — not a one-off patch to the case that triggered it.
