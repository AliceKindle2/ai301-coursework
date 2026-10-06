# Procedure: how this tool grades a PR package

## Read order

1. Read the issue first, to know what behavior was originally reported.
2. Read the plan (`plan.md` or the plan-context block) next, in full, including its `## Deviations` section — this is the boundary everything else gets checked against.
3. Read the PR description next, noting every specific claim it makes about what changed and why.
4. Read the diff (`git diff main...HEAD`, or the bundle's diff section) next, file by file, noting every changed file and hunk.
5. Read the test-evidence section last, comparing it against the plan's test plan as read in step 2.

## Evidence gathering

1. For `diff-matches-plan`: pull the plan's in-scope/out-of-scope statement and its `## Deviations` notes from step 2; pull the full list of changed files and hunks from step 4. Place them side by side: every changed file must be either in-scope, or covered by a named deviation.
2. For `description-matches-diff`: pull every specific claim from the PR description (step 3); pull the actual diff contents (step 4). Check each claim against what the diff actually shows, in both directions (does the diff do what's claimed, and does the diff do anything the description doesn't mention).
3. For `test-evidence-observable`: pull the plan's test plan (step 2) and the test-evidence section (step 5); check whether a concrete before/after result appears, and whether it matches what the test plan said to expect. Also check for the repo's own CI/check results if the package or live PR shows them.
4. For `diff-reviewable`: re-examine the diff and commit list from step 4 for any hunk that does not serve the one bounded change — debug prints, commented-out code, formatting-only changes to untouched logic, or edits to files the plan never named.
5. For `standards-and-template-followed`: pull the repo-facts block's stated PR template sections and contribution/AI-disclosure policy; pull the actual PR description's section-by-section content; check each required section for real content and check for a disclosure statement if the policy calls for one.
6. For `honest-shortfall-disclosed`: cross-reference everything gathered in steps 1-5 for any genuine gap (an edge case the diff doesn't handle, a deviation from the plan, an incomplete test) and check whether the description states it plainly.

## Check execution

1. Grade checks in the order listed in the rubric's table.
2. Grade a check `pass` only when the gathered evidence explicitly satisfies its pass condition — quote the specific fact that decided it.
3. Grade a check `fail` when the evidence contradicts the pass condition, quoting the contradicting fact.
4. Grade a check `unclear` only when the evidence the check names is genuinely absent from the package or live submission, never because closer reading would resolve it.
5. Never grade a check on the PR's length, commit count, or formatting — grade only whether the stated fact holds against the evidence gathered in the previous stage.
6. If a step needed to gather evidence for a check is not covered by this procedure (e.g. no instruction for a missing diff, or an ambiguous template section), report that gap explicitly in the output instead of improvising a step to cover it.

## Verdict assembly

1. List every required check's grade in the order they were executed.
2. If every required check graded `pass`, the verdict is `accept`.
3. If any required check graded `fail` or `unclear`, the verdict is `reject`.
4. When more than one required check fails or is unclear, quote the fact for the first failing/unclear check in the rubric's table order as the deciding check in the output summary — this is the fixed tie-break rule, applied every time, regardless of which failure feels most important.
5. In live mode, after assembling the verdict, hold the draft PR title and description against `voice-guide.md` and report any broken rule in the summary; this never changes the verdict itself unless a rubric check explicitly reads the voice guide.