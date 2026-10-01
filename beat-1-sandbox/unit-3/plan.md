# Plan: README scorer fixture word-count assertion (#63)

## Diagnosis

From my reproduction (posted at https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5922826062):

Running `pytest tests/unit/test_readme_scorer.py -v` shows `22 passed, 1 xfailed`, with `test_readme_with_all_quality_signals` marked `XFAIL`. Forcing it with `--runxfail` shows the real failure: `assert data["word_count"] > 100` fails as `assert 51 > 100`, with the scorer logging `word_count=51, category=minimal`.

The test makes two assertions on the fixture: `word_count > 100` and `word_count_category == "comprehensive"`. Looking at `agent/tools/readme_scorer.py`'s category thresholds, "comprehensive" requires 500 or more words — 100 to 499 words is categorized "adequate," not "comprehensive." The fixture currently has every structural signal the test checks for (installation, usage, badges, demo link, tech stack) but only 51 actual words, well under both thresholds. The fix needs to push the fixture's word count past 500, not just past 100, or the second assertion will still fail even after the first one passes.

## Scope

In scope: the fixture README string inside `test_readme_with_all_quality_signals`, in `tests/unit/test_readme_scorer.py`, and the `@pytest.mark.xfail(...)` decorator on that same test.

Not in scope: `ReadmeScorer`'s word-counting or categorization logic (`agent/tools/readme_scorer.py`) — my repro confirmed it counts and categorizes correctly. Not in scope: any other test in `tests/unit/test_readme_scorer.py` — all 22 others already pass.

## Approach

1. Open `tests/unit/test_readme_scorer.py` and locate the fixture README string inside `test_readme_with_all_quality_signals`.
2. Add enough additional prose across the fixture's existing sections (project description, installation, usage, features, tech stack, demo) to push the total word count past 500, while keeping every structural signal (`has_installation_section`, `has_usage_section`, `has_badges`, `has_demo_link`, `has_tech_stack_section`) detectable and unchanged.
3. Remove the `@pytest.mark.xfail(strict=True, reason="issue #63: ...")` decorator, since the fixture will then legitimately satisfy both assertions it currently fails.

## Test plan

Before: `pytest tests/unit/test_readme_scorer.py -v` reports `22 passed, 1 xfailed`, with `test_readme_with_all_quality_signals` shown as `XFAIL`.

After the fix, the same command should report `23 passed` with no `xfail` anywhere, and `test_readme_with_all_quality_signals` specifically shown as `PASSED`. I'll also re-run with `--runxfail` to confirm the assertions pass on their own merits: `word_count > 100` and `word_count_category == "comprehensive"` (meaning the fixture must land at 500+ words, confirmed via the scorer's log line).

## Risks and unknowns

- I had not initially confirmed the exact word-count threshold for the "comprehensive" category before drafting this plan; I've now checked `agent/tools/readme_scorer.py` directly and confirmed it's 500+ words, not 100+, and adjusted scope/approach above accordingly.
- Adding substantial prose risks accidentally tripping a different section-detection pattern unintentionally; I'll re-run the full test file after the change, not just the target test, to catch this.
- I'm assuming the maintainer's preferred fix is "add fixture prose" rather than "lower the assertion thresholds"; I'm keeping the diff limited to the fixture string and the xfail decorator so a maintainer can easily redirect in review if they'd prefer a different approach.

## Deviations

Nothing changed from the plan's scope or approach. One correction happened during the build: my first attempt at expanding the fixture added only ~220 words, which passed the `word_count > 100` assertion but landed in the `"adequate"` category rather than `"comprehensive"` (which requires 500+ words) — an error traced back to not having confirmed the exact category thresholds before writing the first draft of this plan. I added further prose to push the total to 568 words, after which the test passed exactly as planned: `23 passed`, no `xfail`, `test_readme_with_all_quality_signals` shown as `PASSED`.
