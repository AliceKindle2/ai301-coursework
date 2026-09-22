# Voice guide: how I talk upstream

## Who I am in threads

I'm a student contributor working through a structured course, making my first real open-source contribution. I'm here to investigate and report honestly, not to promise fixes I haven't earned yet. Readers should expect careful, evidence-backed comments from me — nothing overconfident, nothing padded.

## Rules I write by

### Rule: Never promise a fix or a date

I only commit to investigating, not to delivering a solution or a timeline.

- Wrong: "I'll have this fixed by tomorrow!"
- Right: "I'm going to dig into this and report back what I find."

### Rule: State uncertainty plainly

If I'm not sure I've reproduced the actual bug, I say so instead of writing around it.

- Wrong: "Yep, this is definitely the bug, confirmed."
- Right: "I saw similar behavior, but I'm not fully certain it's the same root cause — here's what I observed."

### Rule: Disclose AI assistance where the repo asks for it

If the repo's contribution policy asks for AI-disclosure, I say so plainly rather than skip it or bury it.

- Wrong: (no mention of tooling used, despite a stated disclosure policy)
- Right: "I used an AI coding assistant to help investigate this; all steps below were run and verified by me."

### Rule: Keep the claim comment short and specific

A claim comment names the issue's specifics — not a generic "I'll take this."

- Wrong: "I'll take this one!"
- Right: "I'd like to investigate this — I can see the fixture in test_readme_scorer.py asserts word_count > 100 but the fixture is ~51 words; I'll dig into whether that's the actual bug or something else is going on."

## Things I never post

- A promise of a completed fix or a delivery date.
- A "confirmed reproduced" claim without pasted output/evidence backing it.
- A comment that skips required AI-disclosure when the repo's policy calls for it.
- Vague filler like "just checking in" or "any updates?" with no new information attached.