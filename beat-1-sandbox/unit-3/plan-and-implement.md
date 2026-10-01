# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

AliceKindle2

**Plan comment**

[FILL IN once posted: the permalink]

[FILL IN: paste the exact text you posted — likely close to the draft below, once you've run it through plan-check and revised as needed]

Posting my plan: I'll add more prose content to the fixture README in `test_readme_with_all_quality_signals` (keeping its existing structural sections — installation, usage, badges, demo link, tech stack — intact) so it legitimately exceeds the 100-word threshold the test asserts on, then remove the `xfail` marker since the test will pass for real. This only touches that one fixture string and the xfail decorator; nothing in `ReadmeScorer` itself needs to change, since it's already counting words correctly. I'll re-run `pytest tests/unit/test_readme_scorer.py -v` before and after to confirm.

---

## Your branch

**Branch**

[FILL IN once created: e.g. fix/63-readme-fixture-word-count]

**Evidence**

[FILL IN after the build. Structure:]

Before (from Unit 2 repro):
