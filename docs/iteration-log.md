# Iteration log

Four fixes, each traced back to one specific, dated failure. Company and posting details are generalized here since the underlying application activity is private; the mechanism and the fix are exactly as they happened.

## 1. Boilerplate vs. the actual location field

A job posting's legal boilerplate described "remote" in generic terms that, read at face value, would have passed a remote-eligibility check the role should have failed — the fine print made clear the hiring entity only had a footprint in one country, and it wasn't mine.

**Root cause:** the check was reading the JD's prose instead of the posting's structured location field and legal entity.
**Fix, made standing:** always read the job board's own location field and confirm a hiring entity exists in the relevant country. Never infer eligibility from boilerplate language, however confident it sounds.

## 2. Volume to one employer reads as indiscriminate

Multiple applications went out to the same company on the same day, for adjacent but distinct roles. In hindsight, that's a worse signal than applying to only the strongest-fit one — it reads as spam rather than genuine interest, and whichever application a recruiter opens first becomes the impression that sticks.

**Root cause:** the workflow scored each role independently and had no view of the applicant's own portfolio — how many applications were already in flight to the same place.
**Fix, made standing:** cap applications to a single company within a short window, rank the candidates if more than one clears the bar, and send only the strongest first. The rest stay built and ready rather than going out together.

## 3. A date parsed through a summarizer, not from the source

A web summarization step misread a job posting's timestamp by roughly two years — an easy mistake for a general-purpose summarizer to make with ambiguous date formats, and one that would have quietly failed a "posted within N days" freshness check in the wrong direction.

**Root cause:** dates were being extracted from a rendered, summarized version of the page instead of the posting's own structured data.
**Fix, made standing:** parse posting dates directly from the source (the job board's own API or structured markup) rather than through any intermediate summarization pass.

## 4. Aggregator copy hid a retitle

A role appeared on a general job aggregator under one seniority title. The employer's own applicant-tracking system, checked directly, showed a different, lower title — the aggregator's copy was stale relative to a change the employer had made after the original listing synced.

**Root cause:** trusting an aggregator's cached copy of a listing instead of the employer's own system of record.
**Fix, made standing:** verify title, level, and location against the employer's own ATS whenever one is reachable. Aggregators are a discovery tool, never the source of truth for gate checks.

---

The common shape across all four: something slipped through once, the root cause got named specifically enough to generalize, and the fix became a rule in the standing instructions — not a patch applied only to the case that surfaced it. Every future session inherits the fix automatically, the same way a codebase inherits a bug fix once it's merged rather than re-discovering it each time someone hits the same edge case.
