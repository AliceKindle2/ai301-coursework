# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: The plan states its cause in its Diagnosis/Cause section (usually the first part of the Candidate plan). The repro evidence that must be checked against it lives in the Repro evidence section's numbered steps, timings, and any explicit "Expected"/"Actual" lines. In live mode: the student's draft plan's diagnosis, checked against their own Unit 2 repro comment/report.

What good looks like: The stated cause explains every data point the repro evidence shows, not just the convenient ones. If the repro evidence includes a control or a variant that would rule out a candidate cause (e.g. the delay persists even with the pager removed entirely, or a control case that behaves differently), the diagnosis must be consistent with that data point, not silently contradict it. A diagnosis adopted verbatim from a thread comment without being checked against the repro evidence's own steps and timings does not follow from the evidence, even if it sounds specific and confident.

## Scope

Where it lives: The plan's Scope section, typically naming specific files/functions under an "In scope" heading and what the plan deliberately won't touch under an "Out of scope" or equivalent line.

What good looks like: One bounded change — a specific file or function is named, and a clear boundary is drawn around what else exists nearby but is not being touched. A scope that says "poke around the code," names no specific location, or quietly expands to cover adjacent systems (e.g. fixing a navigation bug but also "cleaning up" the rendering pipeline) is a drive-by rewrite, not a bounded change, even if it's described enthusiastically.

## Executability

Where it lives: The plan's Approach/Changes section — the concrete, usually numbered list of what will actually be done, naming files, functions, call sites, or specific code paths.

What good looks like: A stranger with no other context about the issue could read this section alone and know exactly where to start — a specific function to call, a specific site to edit, a specific sequence of steps. A plan that states only an intention or a goal ("figure out where the undo history lives," "make undo work across toggles") without naming where that work starts is not yet executable; the author would still need to do the investigation before anyone (including the skill reviewing a follow-up PR) could verify the plan was followed.

## Test plan

Where it lives: The plan's Test section, read directly against the Repro evidence's steps and any stated "Expected" behavior.

What good looks like: The test plan either re-runs the exact repro steps and names the specific observable difference expected after the fix (e.g. "at step 3 the color must flip without leaving the view"), or names a new, targeted test tied to the specific reported behavior. "Run the existing test suite and make sure nothing regresses" is not decisive on its own — it says nothing about whether the originally reported behavior would actually be caught by that suite, and doesn't name any new assertion targeting the bug itself.

## Honesty

Where it lives: The plan's Risks/Unknowns section (if present), read against the confidence level of its Diagnosis and Scope sections. In the build phase, this becomes the `## Deviations` heading in `plan.md`.

What good looks like: Any assumption the plan actually rests on that hasn't been independently verified — an unverified thread claim, an untested edge case, an assumption about how a shared code path behaves — is named explicitly as a risk or unknown, rather than folded silently into the diagnosis as if it were settled fact. A plan with real uncertainty that states none is overconfident; a plan that honestly flags "I haven't confirmed X, but my fix should hold because Y" is not weaker for saying so — it's stronger and more trustworthy. The same honesty standard applies to a filled `## Deviations` section: "nothing changed from the plan" is a complete, honest answer when it's actually true; a blank section is not.

## Comms

Where it lives: The plan comment text, read against Thread highlights (specifically any OWNER/MEMBER/COLLABORATOR statement) and against the repo-facts block's stated contribution policy, AI-use disclosure requirements, and any noted constraints (e.g. limited review bandwidth, a preference for small PRs).

What good looks like: The comment acknowledges and either builds on or explicitly disagrees with any maintainer statement already in the thread — it never silently proceeds as if a maintainer hadn't already said something relevant (e.g. "known issue, no current solution" or a stated root cause). If the repo's policy requires AI-assistance disclosure, the comment discloses it plainly and in the commenter's own words, not as a copy-pasted boilerplate line. If CONTRIBUTING notes a constraint like scarce review time, the comment's described scope reflects that constraint (e.g. explicitly keeping the change minimal) rather than ignoring it.