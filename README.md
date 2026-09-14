<h1 align="center">Grounded PM Agent</h1>
<p align="center"><i>A Claude Code agent workspace that runs a technical product manager's own job search, and is held to the same discipline the job itself demands.</i></p>

<p align="center">
  📄 <a href="resume/Sri_Janani_Nagarathinavel_Resume_Public.docx">Resume</a> ·
  💼 <a href="https://linkedin.com/in/sri-janani-nagarathinavel-80003659">LinkedIn</a> ·
  ✉️ srijanani.vel@gmail.com
</p>

---

## What this is

Most "I use AI tools" answers in a PM interview describe usage: a copilot that drafted an email, a summary it wrote. This repository documents something narrower and more specific: **an agent workspace I designed, with a gate before every expensive output and a rule that no claim survives without a source.**

The domain it runs on is my own job search — resume tailoring, JD scoring, interview prep — chosen because it is the one problem space where I have full context on what is true, so I can catch the agent (and myself) the moment it drifts from evidence into a plausible-sounding guess.

**What is real here:** every design decision below is one I made and can defend in a follow-up question. Claude Code writes the text and runs the commands; I wrote the rules, the rubric, and the memory structure, and I make every judgment call the workflow surfaces. The actual private workspace (comp targets, personal notes, live application state) stays private — what's public is the *design*, reproduced here with placeholder values so the mechanism is inspectable without exposing anything of mine.

## The problem I was actually solving

Tailoring a resume or a story for a specific JD is exactly the kind of task a language model is good at and bad for: it will happily generate a plausible metric, a plausible tool name, a plausible sentence about "led a cross-functional team of 40" if the JD asks for one. That failure doesn't show up in a demo. It shows up two interview rounds later, when someone asks a follow-up question the fabricated claim can't survive.

So the design problem wasn't "how do I get better resume text out of a model." It was **how do I make a model structurally incapable of writing a claim it can't source** — not through a better-worded prompt, but through a workflow that blocks the unsourced path entirely.

## How it's built

| Component | What it does |
|---|---|
| **Standing instructions file** | Read at the start of every session. States the one rule everything depends on ("nothing goes in an output that isn't in the evidence file"), the hard constraints that gate any work at all, and a running list of facts that are easy to get wrong. See [`templates/project-instructions-sample.md`](templates/project-instructions-sample.md). |
| **A gated scoring rubric, not a suggestion** | Before any tailoring happens, the agent has to run a multi-stage fit check — hard pass/fail gates first, then a weighted score — and report the result before writing anything. If a gate is unconfirmed, the workflow stops and the agent has to ask, not assume. See [`templates/fit-check-rubric-template.md`](templates/fit-check-rubric-template.md). |
| **A single evidence file, and a do-not-quote list next to it** | Every fact that can appear in output lives in one file. Anything a JD asks for that isn't in that file goes into an explicit "cannot evidence" list instead of getting softened into the resume. See [`docs/grounding-example.md`](docs/grounding-example.md) for a real instance of this catching a near-miss. |
| **A packaged, repeatable skill for the actual tailoring pipeline** | Company research → keyword extraction against the evidence file → resume draft, in that order, every time, instead of improvising the sequence per JD. |
| **Append-only session memory, separate from git** | Git records *what* changed. A separate run log records *why* — the reasoning behind a decision, what got corrected, what's still open — because that's the part that doesn't survive in a diff and the part a fresh session actually needs to pick the work back up correctly. |

## A concrete example: the memory closing its own gap

Early on, a JD's boilerplate location clause would have let a US-based role pass a remote-eligibility check it should have failed — the JD used generic "remote" language that, read carelessly, looked fine. The fix wasn't a one-off correction to that JD. It was a rule change: read the job board's actual location field and confirm a hiring entity exists in the right country, never the boilerplate paragraph. That rule is now in the standing instructions, and every session since inherits it automatically. [`docs/iteration-log.md`](docs/iteration-log.md) has more of these, all anonymized the same way.

That loop — a specific failure becomes a general rule, logged with the reasoning, inherited by every future session — is the actual product decision underneath this build. It is the same instinct as version-controlling a spec, applied to an agent's judgment instead of its code.

## What this doesn't claim to be

- **Not a shipped product.** One user, no adoption numbers, no eval set. I'm describing a personal workflow, not a launch.
- **Not agent-framework or tool-calling engineering.** I designed the rules, the gates, and the memory structure; Claude Code executes them. That's a meaningfully different skill from building an agent runtime, and I'm not blurring the two.
- **Where I'd take it next**, if this were a product instead of a personal tool: a proper eval harness against known-good tailoring outcomes, a structured way to score how well a session's output actually survived an interview (right now that loop is manual, via the debrief step), and replacing the single-file evidence store with something queryable as the fact base grows past what fits in one document.

## Repo layout

```
README.md                              — this file
resume/                                — the resume this workspace produces, phone number withheld for a public link
docs/architecture.md                   — deeper walkthrough of each component
docs/grounding-example.md              — a specific claim the evidence rule blocked, and what happened instead
docs/iteration-log.md                  — four anonymized instances of a failure becoming a standing rule
templates/project-instructions-sample.md   — a sanitized version of the standing-instructions file
templates/fit-check-rubric-template.md     — a sanitized version of the gated scoring rubric
```
