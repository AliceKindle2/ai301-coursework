# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-matches-evidence | The plan's stated cause, read against the repro evidence's steps, timings, and artifacts | Passes when the stated cause explains the specific behavior the repro evidence shows, including any data point that would rule out a competing cause. Fails when the cause is adopted from a thread comment without being checked against the repro evidence, or when it explains a different symptom than what was reproduced | required |
| scope-bounded | The plan's scope statement | Passes when it names the specific file(s) or function(s) to be changed and explicitly states what it will not touch. Fails when the change is an open-ended exploration ("poke around the code") or when it reaches beyond the one behavior the issue and repro evidence describe | required |
| executable-by-a-stranger | The plan's change/approach section | Passes when a reader with no other context could start making the named edit from the plan alone — a specific site, a specific mechanism. Fails when the plan states only an intention or a goal with no concrete starting point | required |
| test-plan-observable | The plan's test plan, read against the repro evidence's steps | Passes when the test plan re-runs or extends the exact repro steps, or names a specific targeted test, with a stated observable result after the fix. Fails when it names only "run the existing suite" with no step tied to the actual reported behavior | required |
| unknowns-stated-honestly | The plan's risks/unknowns section, read against the diagnosis and scope | Passes when open questions or untested assumptions the plan actually has are named as such. Fails when the plan presents a guess or an unverified thread claim as settled fact with no acknowledgment of the uncertainty | required |
| conventions-respected | The plan comment, read against the repo-facts contribution/AI policy and thread highlights | Passes when any stated AI-disclosure requirement is met in the comment's own words, any stated reviewer-bandwidth or similar constraint is reflected in the change's size, and the comment does not silently contradict a maintainer's prior statement in the thread. Passes by default when the repo states no such policy and the thread has no maintainer statement to reconcile | required |

## Verdict rule

The verdict is `accept` (ready to build from) when every `required` check grades `pass`, and `reject` (hold) when any `required` check grades `fail` or `unclear`. A required check graded `unclear` counts as a fail: the evidence these checks name is present in every package, so `unclear` means the signal genuinely could not be found, and a plan whose safety cannot be verified is not one to build from yet.

The output's `verdict` field must be exactly `accept` or `reject` — never `ready` or `hold`.