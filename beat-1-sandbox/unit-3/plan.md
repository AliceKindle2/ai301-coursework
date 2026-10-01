# Plan: README scorer fixture word-count assertion (#63)

## Diagnosis

From my Unit 2 reproduction (posted at https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5922826062):

> Test output: `tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals XFAIL` — `22 passed, 1 xfailed in 2.84s`
>
> I confirmed the fixture's actual word count directly: `51`. This matches the issue's stated `assert 51 > 100` exactly.

The test is marked `@pytest.mark.xfail(strict=True, reason="issue #63: README scorer fixture is too short for its own word-count assertion")`. Forcing the underlying assertion with `--runxfail` (confirmed in my Unit 2 repro) shows `assert data["word_count"] > 100` fails as `assert 51 > 100`, with the scorer's own log line confirming `word_count=51, category=minimal`.

The fixture README inside `test_readme_with_all_quality_signals` contains every structural quality signal the test checks for (installation section, usage section, badges, demo link, tech stack section), but almost all of its length is markdown syntax (headers, code fences, bullet points) rather than actual prose — so its true word count is only 51. `ReadmeScorer` is measuring and categorizing correctly here; the fixture itself simply does not contain the 100+ words of prose needed to legitimately satisfy the assertion it's being tested against. This is a fixture-content problem, not a scorer logic bug. No part of my own repro evidence contradicts this: the failure is reproducible, deterministic, and exactly matches the issue's stated numbers.

## Scope

In scope: the fixture README string inside `test_readme_with_all_quality_signals`, in `tests/unit/test_readme_scorer.py`. The fix adds enough additional prose content to that fixture so its word count legitimately exceeds 100, while preserving every structural signal the test already checks for. The `@pytest.mark.xfail(...)` decorator on this same test is also in scope, since it must be removed once the fixture legitimately passes.

Not in scope: `ReadmeScorer`'s word-counting or categorization logic (`agent/tools/readme_scorer.py`) — my repro confirmed it is already counting correctly. Not in scope: any other test in `test_readme_with_all_quality_signals.py` — all 22 others already pass. Not in scope: any other fixture or `xfail` marker elsewhere in the test suite.

## Approach

1. Open `tests/unit/test_readme_scorer.py` and locate the fixture README string inside `test_readme_with_all_quality_signals` (the string currently totaling 51 words, structured as a project title, description, Installation, Usage, Features, Tech Stack, badges, and Live Demo sections).
2. Add 2-4 additional sentences
