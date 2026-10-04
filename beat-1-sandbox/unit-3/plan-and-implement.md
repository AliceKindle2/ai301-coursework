# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

---

## Posted upstream

**GitHub username**

AliceKindle2

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5984369149

Posting my plan: based on my reproduction above (word_count=51, with the test requiring word_count > 100 and word_count_category == "comprehensive", which needs 500+ words per readme_scorer.py's thresholds), I'll add more prose content to the fixture README in test_readme_with_all_quality_signals — keeping its existing structural sections (installation, usage, badges, demo link, tech stack) intact — so it legitimately exceeds 500 words, then remove the xfail(strict=True) marker since the test will pass for real at that point. This only touches that one fixture string and the xfail decorator; ReadmeScorer itself doesn't need to change, since my repro confirmed it's already counting and categorizing correctly. I'll re-run pytest tests/unit/test_readme_scorer.py -v before and after to confirm.

---

## Your branch

**Branch**

fix/63-readme-fixture-word-count

**Evidence**

Before:

pytest tests/unit/test_readme_scorer.py -v -k "test_readme_with_all_quality_signals" --runxfail
...
FAILED tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals - assert 51 > 100
------------------------------------------------ Captured stdout call -------------------------------------------------
2026-10-01 16:28:43 [info ] readme_scored category=minimal score=0.8717142857142858 word_count=51
1 failed, 22 deselected in 0.56s


After:

pytest tests/unit/test_readme_scorer.py -v
...
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED
23 passed in 0.40s

pytest tests/unit/test_readme_scorer.py -v -k "test_readme_with_all_quality_signals" --runxfail
...
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED
1 passed, 22 deselected in 0.29s


## Eval iterations

**Run history**

1. First full run: 19/19 scored items agreed, but 1 package (pkg-07) errored with an invalid verdict string ("hold" instead of "accept"/"reject") — a wording bug in the verdict rule, not a reasoning error. Not a valid full run; not saved.
2. Fixed the verdict rule to emit `accept`/`reject` literally instead of `ready`/`hold`. Full run: 19/20 agreement, all category floors passed (`clear-accept 6/7`, `scope-creep 4/4`, `thread-convention 2/2`, `unbuildable 3/3`, `wrong-cause 4/4`). This matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-14` — gold label: `accept`. My rubric's verdict was `reject`, a false negative, failing on `executable-by-a-stranger`. [STILL NEEDS: open pkg-14's actual bundle file from your Unit 3 materials' eval/packages/ folder and describe what's actually in it, so this is an honest account rather than a guess.]

**Check rationale**

From `rubric.md`, the "diagnosis-matches-evidence" check's pass condition, as currently written:

> Passes when the stated cause explains the specific behavior the repro evidence shows, including any data point that would rule out a competing cause. Fails when the cause is adopted from a thread comment without being checked against the repro evidence, or when it explains a different symptom than what was reproduced.

It reads this way because of what we found grading `calib-03` in the Unit 3 activity: a plan adopted a specific, confident-sounding cause directly from a non-maintainer's thread comment (pager key-binding registration) without checking it against the repro evidence's own timings, which actually showed the slowdown persisted even with no pager involved at all — pointing at syntax highlighting, not pager navigation. The sample rubric's plain "does the plan say what causes the bug" check passed that plan anyway. I rewrote the check to require consistency with every data point in the repro evidence, not just plausibility, specifically so a confident wrong-cause plan can't pass just because it names a cause.

**Trade-offs**

Requiring the diagnosis to be checked against every repro-evidence data point, rather than just "names a plausible cause," means my rubric will correctly reject a plan whose cause sounds reasonable and well-written but hasn't actually been cross-checked against the evidence — which is exactly the trade I wanted, since that's the failure mode calib-03 demonstrated. The cost is that this check requires the repro evidence section to actually contain enough specific data points (timings, controls, variants) to rule causes in or out; a package with a thin repro evidence section could cause this check to grade `unclear` more often than it should, even for a genuinely correct diagnosis, simply because there isn't enough evidence present to confirm the match either way.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in `tools/plan-check/`.
