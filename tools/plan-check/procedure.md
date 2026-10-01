# Procedure: how this skill grades a plan package

## Read order

1. Read the issue title and body first, to know what behavior is being reported.
2. Read Thread highlights next, noting each commenter's author_association (OWNER/MEMBER/COLLABORATOR statements carry weight the others don't).
3. Read Repro evidence next: the environment, the numbered steps, and any stated "Expected"/"Actual" lines — this is the ground truth every later check compares against.
4. Read the Candidate plan in full (diagnosis, scope, approach, test plan, risks/unknowns).
5. Read the Candidate plan comment last, since it is graded against everything read above it.

## Evidence gathering

1. For `diagnosis-matches-evidence`: pull the plan's stated cause verbatim, and pull every timing, artifact, and "Expected"/"Actual" line from Repro evidence. Place them side by side and check whether any repro data point is left unexplained or contradicted by the stated cause.
2. For `scope-bounded`: pull the exact file/function names and the explicit "will not touch" statement from the plan's scope section.
3. For `executable-by-a-stranger`: pull the specific site/mechanism named in the plan's approach section — the concrete line someone could start from.
4. For `test-plan-observable`: pull the plan's test section, and pull Repro evidence's steps; check whether the test plan's steps overlap with or extend the actual repro steps, and whether a stated observable result after the fix is present.
5. For `unknowns-stated-honestly`: pull the plan's risks/unknowns section (if present) and compare it against any claim in the diagnosis or scope that rests on an untested assumption or an unverified thread comment.
6. For `conventions-respected`: pull the repo-facts contribution/AI-policy line, the full plan comment text, and any maintainer/collaborator statement from Thread highlights.

## Check execution

1. Grade checks in the order listed in the rubric's table.
2. Grade a check `pass` only when the gathered evidence explicitly satisfies the pass condition as written — quote the specific fact that decided it.
3. Grade a check `fail` when the evidence contradicts the pass condition, quoting the contradicting fact from the package.
4. Grade a check `unclear` only when the evidence the check names is genuinely absent from the package, never because closer reading would resolve it.
5. Never grade a check on the plan's confidence, length, formatting, or number of headings — grade only whether the stated fact holds against the evidence gathered in the previous stage.
6. A check does not require re-reading the whole package once its specific evidence has been gathered in the Evidence gathering stage.

## Verdict assembly

1. List every required check's grade in the order they were executed.
2. If every required check graded `pass`, the verdict is `accept`.
3. If any required check graded `fail` or `unclear`, the verdict is `reject`.
4. List preferred checks' grades separately; note that they do not change the verdict.
5. In the output's evidence field for the check that decided the verdict (the first failing/unclear required check, or — if all passed — the check most central to the plan's soundness), quote the specific fact from Evidence gathering that drove the grade.