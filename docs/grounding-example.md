# A grounding failure, caught before it shipped

This is a real instance, described generically enough to stay evidence-only in the public version of this repo.

## The setup

Part of my product background involves a feature area where usage was tracked through an internal analytics tool — funnel stages like landing on a feature page, clicking in, activating it, and continuing to use it. I used that tool regularly while the feature was live and made real decisions from what it showed. By the time I came to write this up for a resume, though, my access to that tool was gone. I could describe the practice from memory; I could not pull a current number.

## What the model wanted to write

Given a JD asking for "data-driven decision making," the natural next sentence for a language model to generate is something like *"drove a 34% increase in feature adoption through analytics-informed iteration."* It reads well. It's the shape of sentence every PM resume has. And I have no way to stand behind that specific number, because I no longer have access to the source that would confirm or deny it.

## What the grounding rule does instead

The evidence file for this workspace carries an explicit boundary note next to this exact topic: *"no longer has access to any figures and cannot quote a number — do not estimate one."* That line exists specifically so a future session (or a future me, tired and tailoring the tenth resume of the week) doesn't fill the gap with something plausible.

The rule forces the qualitative version instead: describe the funnel that was actually watched, describe a real decision the data drove (in this case, catching an early drop-off point and changing the rollout approach in response), and stop there. No invented percentage, no rounded-up estimate, no "approximately." If a number can't survive "can you send me the dashboard," it doesn't go on the page.

## Why this is the interesting part

Anyone can tell a model not to lie. The design choice here was making the *boundary itself* a persistent, structural fact — written once, next to the claim it protects, inherited by every session from then on — rather than something I have to remember to catch by re-reading the output every single time. That's the difference between grounding as a rule and grounding as a hope.
