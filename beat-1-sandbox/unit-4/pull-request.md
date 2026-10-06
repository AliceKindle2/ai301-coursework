# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/95

**Branch**

fix/63-readme-fixture-word-count

---

## Eval iterations

**Run history**

One full run: 18/20 agreement, all category floors passed (`clear-accept 5/7`, `not-tested 4/4`, `silent-drift 4/4`, `standards-wall 2/2`, `unreviewable 3/3`). This matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-16` — gold label: `accept`. My rubric's verdict was `reject`, a false negative, failing on `description-matches-diff` and `test-evidence-observable`.

The PR fixes `minikube image load` silently exiting 0 on a guest-side failure. Its description and diff match the plan's scope closely: `DoLoadImages` now returns an aggregated error when every target machine fails, and `cmd/image.go` surfaces it and exits non-zero — exactly what the plan named. Its Test evidence section shows a real before/after transcript (corrupt tarball: exit 1 with a printed error; valid tarball control: exit 0, image present) plus `go test` passing on the touched packages, matching the plan's test plan.

Two things likely drove my rubric's stricter read. First, the diff's shown hunk for `cache_images.go` references `err` inside the loop (`for _, m := range machines { if err != nil {`) with no assignment visible in the excerpt — the diff as presented is slightly incomplete, so a check that insists every description claim be directly verifiable in the diff text itself (rather than trusted from the prose) can't fully confirm the aggregation logic from what's shown, and `unclear` defaults to fail in my verdict rule. Second, my `test-evidence-observable` check wants the specific previously-failing behavior shown passing; the PR's evidence shows the CLI-level exit codes changing as expected, but doesn't separately call out the new unit test (`TestDoLoadImagesAllFailedReturnsError`) actually running and passing by name — only a general "`go test` passes" statement covering the whole package. My rubric reads that generality as less specific than the plan's own test plan asked for, even though the CLI-level before/after is itself strong, legible evidence.

Reading it again now, I think gold's `accept` is the better call: the diff snippet's awkward excerpt is a presentation artifact of the bundle, not a real gap in the actual PR, and the CLI-level before/after is substantive evidence even without naming the new unit test explicitly. This is the clearest miss in my eval run and points at a real brittleness: my checks don't distinguish "evidence is genuinely thin" from "evidence is solid but phrased more generally than the plan's own wording."

**Check rationale**

From `rubric.md`, the "diff-matches-plan" check's pass condition, as currently written:

> Passes when every changed file falls inside the plan's stated in-scope boundary, or is explicitly accounted for in a recorded deviation note. Fails when the diff touches files or behavior outside both the plan's scope and its deviations, with no note explaining the gap (silent drift, in either direction — doing more than planned, or less with nothing said).

This check is written to require checking the entire diff against the entire plan's scope, not just whether the specifically-claimed fix works. I calibrated this against the Unit 4 activity's `calib-03` package: a PR whose core fix worked perfectly and passed every test, but which also silently rewrote an unrelated file with no deviation note anywhere. A rubric that only checked "does the claimed fix work" would have passed that PR; checking every changed file against the plan's named scope catches the undisclosed extra file instead. Running this check against my own real PR (#95) proved its value directly: it caught an unplanned reformatting hunk in an unrelated test (`test_overall_score_calculation`), surfaced by a version mismatch between the repo's pinned pre-commit `black` (24.1.0) and the newer `black` installed elsewhere in the project — exactly the kind of silent, out-of-scope diff change this check exists to catch, and something I would not have investigated and understood without the check forcing the question.

**Trade-offs**

Requiring every changed file to be explicitly covered by either the plan's scope or a deviation note means a PR with a genuinely trivial, harmless incidental change (a one-line formatting adjustment from a linter running on the whole file, say) can fail this check even when the core fix is otherwise excellent — the check doesn't distinguish "a drive-by refactor of unrelated logic" from "an incidental formatter touch with no behavioral effect." `pkg-16` shows the same trade-off from a different angle: my `test-evidence-observable` check's insistence on specific, literal confirmation (rather than crediting strong general evidence) produced a false reject on an otherwise well-evidenced PR. I accept both costs because the alternative — letting ambiguous or general-sounding evidence pass on good faith — is exactly what let `calib-03`'s hidden rewrite through in the Unit 3 activity, and in my own PR, this same strictness forced me to find and understand a real, previously-invisible tooling mismatch in the repository rather than silently shipping a change I didn't fully understand.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/pr-precheck/`.
