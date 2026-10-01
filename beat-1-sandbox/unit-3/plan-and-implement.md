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

https://github.com/AliceKindle2/ai301-coursework/blob/main/beat-1-sandbox/unit-3/comment.md

Posting my plan: based on my reproduction above (word_count=51, with the test requiring word_count > 100 and word_count_category == "comprehensive", which needs 500+ words per readme_scorer.py's thresholds), I'll add more prose content to the fixture README in test_readme_with_all_quality_signals — keeping its existing structural sections (installation, usage, badges, demo link, tech stack) intact — so it legitimately exceeds 500 words, then remove the xfail(strict=True) marker since the test will pass for real at that point. This only touches that one fixture string and the xfail decorator; ReadmeScorer itself doesn't need to change, since my repro confirmed it's already counting and categorizing correctly. I'll re-run pytest tests/unit/test_readme_scorer.py -v before and after to confirm.

---

## Your branch

**Branch**

https://github.com/AliceKindle2/ai301-coursework/tree/main/beat-1-sandbox

**Evidence**

● The issue has no maintainer comments and docs/CONTRIBUTING.md has no AI policy, so I have what I need to grade.

  Grades:

  - diagnosis-matches-evidence: pass. The plan's cause ("51 actual words, well under both thresholds") matches your
    posted repro (assert 51 > 100, word_count=51, category=minimal). The 500+ threshold for "comprehensive" is real:
    agent/tools/readme_scorer.py:70-73. It also covers the second assertion, which the issue body doesn't spell out.
  - scope-bounded: pass. It names one fixture string and one xfail decorator in tests/unit/test_readme_scorer.py. It
    explicitly leaves out ReadmeScorer logic and the other 22 tests.
  - executable-by-a-stranger: pass. It gives a specific test, a specific mechanism (add prose to push past 500 words
    while keeping the five structural signals) and the specific decorator to remove.
  - test-plan-observable: pass. It re-runs your repro command, expects the before state 22 passed, 1 xfailed to become
    23 passed with that test PASSED, and adds a --runxfail check against the scorer's log line.
  - unknowns-stated-honestly: pass. It flags the risk of tripping section-detection patterns, and the assumption that a
    maintainer would rather "add fixture prose" than "lower thresholds." The Deviations section honestly records the
    ~220-word first attempt that landed in "adequate."
  - conventions-respected: pass (by default). docs/CONTRIBUTING.md has no AI-disclosure or review-bandwidth policy. All
    6 thread comments are from students (NONE), so there's no maintainer statement to reconcile.

  Voice-guide notes on the comment (these don't affect the verdict):
  - "State uncertainty plainly": the plan admits you're assuming fixture prose beats lowering the thresholds, but the
    comment doesn't. One clause would fix it, like "if maintainers would rather adjust the assertion instead, happy to
    redirect."
  - "Never promise a fix or a date": no date is given, and "I'll add…" is a statement of plan, not a promise of
    delivery. Fine.
  - "Keep the comment short and specific": met. It names 51 words, the 500+ threshold, the exact test and the decorator.

  Gaps in procedure.md:
  - It only describes the eval bundle's sections ("Thread highlights", "Repro evidence", "repo-facts"). It never says
    where these live in live mode, or what to do if a source isn't available. gh isn't installed here, so I used the
    public GitHub API instead.
  - It doesn't say which file counts as the repo's contribution policy. I used docs/CONTRIBUTING.md.

  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
    "checks": [
      {"name": "diagnosis-matches-evidence", "grade": "pass", "evidence": "Plan: 'only 51 actual words, well under both
  thresholds' matches repro 'assert 51 > 100 ... word_count=51, category=minimal'; 500+ comprehensive threshold verified
  at readme_scorer.py:70-73"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "In scope: fixture string in
  test_readme_with_all_quality_signals + its xfail decorator; Not in scope: ReadmeScorer logic and the other 22 tests"},
      {"name": "executable-by-a-stranger", "grade": "pass", "evidence": "Approach names the test, adds prose past 500
  words keeping the five has_* signals, and removes @pytest.mark.xfail(strict=True, reason=\"issue #63: ...\")"},
      {"name": "test-plan-observable", "grade": "pass", "evidence": "Re-runs repro command: '22 passed, 1 xfailed' ->
  '23 passed', test shown PASSED, plus --runxfail confirming category == 'comprehensive' via log line"},
      {"name": "unknowns-stated-honestly", "grade": "pass", "evidence": "'I'm assuming the maintainer's preferred fix is
  \"add fixture prose\" rather than \"lower the assertion thresholds\"' and section-detection risk named"},
      {"name": "conventions-respected", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states no AI-disclosure or
  bandwidth policy; all thread commenters are author_association NONE, so no maintainer statement to reconcile"}
    ],
    "verdict": "accept"
  }

 
platform win32 -- Python 3.12.10, pytest-9.0.3, pluggy-1.6.0 -- 
cachedir: .pytest_cache
rootdir: C:\Users\Downloads\pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: anyio-4.13.0
collected 23 items

tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED                  [  4%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_no_content PASSED                           [  8%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_only_title PASSED                           [ 13%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_minimal PASSED                      [ 17%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_adequate PASSED                     [ 21%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_comprehensive PASSED                [ 26%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_installation_section_detection PASSED                   [ 30%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_usage_section_detection PASSED                          [ 34%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_setup_keyword_counts_as_installation PASSED             [ 39%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_quickstart_counts_as_usage PASSED                       [ 43%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_badge_detection PASSED                                  [ 47%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_demo_link_detection PASSED                              [ 52%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_tech_stack_section_detection PASSED                     [ 56%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_technologies_keyword_counts PASSED                      [ 60%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_overall_score_calculation PASSED                        [ 65%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_missing_readme_content_key PASSED                       [ 69%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_result_has_all_required_fields PASSED                   [ 73%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_case_insensitive_section_detection PASSED               [ 78%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_whitespace_only_readme PASSED                           [ 82%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_example_keyword_counts_as_usage PASSED                  [ 86%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_score_scales_with_word_count PASSED                     [ 91%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_try_it_as_demo_indicator PASSED                         [ 95%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_built_with_counts_as_tech_stack PASSED                  [100%]

================================================= 23 passed in 0.40s ==================================================
PS C:\Users\Downloads\pathreview-ai301-fa26-s1> python3 -m pytest tests/unit/test_readme_scorer.py -v -k "test_readme_with_all_quality_signals" --runxfail
================================================= test session starts =================================================
platform win32 -- Python 3.12.10, pytest-9.0.3, pluggy-1.6.0 -- C:\Users\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe
cachedir: .pytest_cache
rootdir: C:\Users\Downloads\pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: anyio-4.13.0
collected 23 items / 22 deselected / 1 selected

tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED                  [100%]

========================================== 1 passed, 22 deselected in 0.29s ===========================================

Before (from Unit 2 repro):

platform win32 -- Python 3.12.10, pytest-9.0.3, pluggy-1.6.0 -- C:\Users\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe
cachedir: .pytest_cache
rootdir: C:\Users\Downloads\pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: anyio-4.13.0
collected 23 items / 22 deselected / 1 selected

tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals FAILED                  [100%]

====================================================== FAILURES =======================================================
________________________________ TestReadmeScorer.test_readme_with_all_quality_signals ________________________________

self = <tests.unit.test_readme_scorer.TestReadmeScorer object at 0x0000012C428AF6E0>
scorer = <agent.tools.readme_scorer.ReadmeScorer object at 0x0000012C428D5FA0>

    @pytest.mark.xfail(
        strict=True,
        reason="issue #63: README scorer fixture is too short for its own word-count assertion",
    )
    def test_readme_with_all_quality_signals(self, scorer):
        """Test README with all quality signals returns high score."""
        readme = """
        # Project Name
        A comprehensive project description.

        ## Installation
        ```bash
        pip install package
        ```

        ## Usage
        ```python
        import package
        package.run()
        ```

        ## Features
        - Feature 1
        - Feature 2
        - Feature 3

        ## Tech Stack
        - Python 3.9
        - FastAPI
        - PostgreSQL

        ![Build Status](https://example.com/badge.svg)
        ![Coverage](https://example.com/coverage.svg)

        ## Live Demo
        [Try it here](https://demo.example.com)
        """

        result = scorer.execute({"readme_content": readme})

        assert result.success is True
        data = result.data
        assert data["has_readme"] is True
>       assert data["word_count"] > 100
E       assert 51 > 100

tests\unit\test_readme_scorer.py:60: AssertionError
------------------------------------------------ Captured stdout call -------------------------------------------------
2026-10-01 16:28:43 [info     ] readme_scored                  category=minimal score=0.8717142857142858 word_count=51
=============================================== short test summary info ===============================================
FAILED tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals - assert 51 > 100
========================================== 1 failed, 22 deselected in 0.56s ===========================================
PS C:\Users\aaske\Downloads\pathreview-ai301-fa26-s1>
