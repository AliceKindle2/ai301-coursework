# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63

**Verdict output**

All three candidates are in the scoped repo (codepath/pathreview-ai301-fa26-s1). Graded each independently against
rubric.md; all three pass every required check, so all three are accept.

Repo-level evidence (shared by all three)
- Maintainer active: last default-branch commit 2026-09-16 by Aburke225 (COLLABORATOR) — 2 days old, threshold 120.
- Repo in active use: 10 commits in the last 90 days; last push 2026-09-16 (2 days), not archived.
- Maintainer responsive (preferred): Aburke225 replied on #52 and #43 on 2026-09-16, ~6 days after they were opened — inside 60.
- Not duplicated effort: state=open PR list is empty (0 open PRs), and no cross-referenced events on any of the three timelines.

Ranked read-out (accepted)

1. #63 — README scorer test fixture too short for its own word-count assertion. Carries the maintainer's own good
   first issue label; the deliverable is a single fixture edit in tests/unit/test_readme_scorer.py with an exact
   failure to chase (assert 51 > 100) and no production code involved.
2. #64 — Relevance scorer "partial overlap" fixture actually has full overlap. Also good first issue, also one fixture
   file (tests/unit/test_relevance_scorer.py, assert 1.0 < 0.9), but fixing it means understanding how the scorer
   computes keyword coverage well enough to construct a genuinely partial overlap — a step more design than #63.
3. #59 — Faithfulness checker scores claims unsupported on different wording. Narrow and reproducible (_is_supported()
   in rag/evaluator/faithfulness_checker.py, assert 0.0 > 0.5 in test_multiple_context_chunks), so it passes scope on
   the "one specific reproducible bug" clause — but it is the only one of the three without a good first issue label,
   and it asks for a replacement support heuristic in production code rather than a fixture correction.

Two things worth flagging about the rubric rather than the run:

- scope.md's fit profile is still the placeholder ((Write a few sentences here.)), so I could not rank on fit. All
  three tie on preferred checks (4/4 each), and the rubric's tie-break is exhausted at that point, so the ordering
  above falls back to the maintainer's good first issue label and the size of the deliverable. Fill in the profile and
  the ranking gets a real basis.
- The rubric has no contribution-policy check, so the fifth surface in the evidence guide went ungraded.
  docs/CONTRIBUTING.md exists in the repo; no AI_POLICY.md or AGENTS.md. I did not let this touch any verdict.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
  "checks": [
    {"name": "Maintainer active", "grade": "pass", "evidence": "Last main commit 2026-09-16 by Aburke225 (COLLABORATOR), 2 days before 2026-09-18"},
    {"name": "Maintainer responsive", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) replied on issues #52 and #43 on 2026-09-16, ~6 days after they opened"},
    {"name": "Repo in active use", "grade": "pass", "evidence": "10 default-branch commits within the last 90 days; last push 2026-09-16, not archived"},
    {"name": "Issue not stale", "grade": "pass", "evidence": "created 2026-09-10, updated 2026-09-10 — 8 days old"},
    {"name": "Scope fits newcomer", "grade": "pass", "evidence": "Labeled 'good first issue'; one fixture in tests/unit/test_readme_scorer.py, not an index of linked issues"},
    {"name": "Scope not vague", "grade": "pass", "evidence": "'asserts word_count > 100 ... but its fixture README contains only ~51 words' with a pytest repro"},
    {"name": "Not already claimed or worked", "grade": "pass", "evidence": "assignees [], 0 comments, timeline shows only 4 label events"},
    {"name": "Not duplicated effort", "grade": "pass", "evidence": "0 open PRs in the repo; no cross-referenced events on the timeline"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. 11/20 — category floor failed on `clear-accept` (0/8).
2. 14/20 — category floor failed on `policy` (0/1); introduced 3 new false-accepts.
3. 19/20 — all category floors passed (`claimed 4/4`, `clear-accept 7/8`, `dead-repo 3/3`, `policy 1/1`, `scope 4/4`). This matches the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-12` — gold label: `reject`. After the second rubric revision, my rubric's verdict was `accept`, a false positive. At that point, the "Not already claimed" check only looked for explicit claim language ("I'll take this") or an assigned GitHub user, and neither was present in the thread. But a contributor (`jrings`) had already commented showing real, specific progress on the fix — they had extracted the underlying percent-finished data, attached a screenshot of a working partial version, and asked a targeted follow-up question about implementing a stacked bar. That is a much stronger signal that the issue is already being worked than a bare expression of interest, even without a formal claim comment or assignee. My rubric read the issue as open because it was only checking for claim language, not for evidence of work already in progress.

**Check rationale**

From `rubric.md`, the "Not already claimed or worked" check's pass condition, as currently written:

> Fails if: (a) a comment shows actual progress already made (code, screenshots, "here's what I have so far"), (b) explicit claim language ("I'll take this," "assigned to me"), (c) GitHub shows an assignee, or (d) the thread shows 3+ prior claim-then-abandon cycles (someone claims, then is unassigned for inactivity, repeatedly) — a pattern suggesting the issue is a known trap even if currently open. Plain expressions of interest ("I'd like to help," "any guidelines?") with no follow-through do NOT count as a claim.

It is written this broadly because the earlier version, which only matched explicit claim phrases, missed `issue-12`: a contributor had shown real progress without using any claim language. Adding condition (a) closes that gap. Condition (d) was added separately after `issue-15` showed a five-year history of repeated claim-then-abandon cycles that leaves the issue technically unclaimed right now but a known trap in practice.

**Trade-offs**

Requiring "actual progress" evidence, rather than any comment at all, to trigger a fail means the check still passes plain expressions of interest ("I'd like to help," "any guidelines?") through as not-claimed — which is deliberate, since penalizing someone for asking a question would reject issues that are genuinely still open. The trade-off is that a contributor who has done real work but described it vaguely, without anything I'd read as "code, screenshots, or here's what I have so far," could still slip past this check as not-claimed. I accept that risk because the alternative (treating any comment as a claim) would have caused far more false rejects than the false accepts it prevents, given how many of the 20 eval issues have comment threads full of people simply asking to help.

---

## Selection rationale

**Selection rationale**

1. Of the three accepted candidates, #63 is the smallest and most contained: a single test-fixture edit with a concrete, already-reproducible failure. That fits the time I have for a first contribution better than #64 (which needs more design thinking about how the scorer computes overlap) or #59 (a production-code fix without a "good first issue" label).
2. The verdict correctly identified that the repo is actively maintained and that none of the three candidates are already claimed or duplicated by an open PR — that part I trust. What I weighed beyond the rubric is that #63 and #64 both carry the maintainer's own "good first issue" label while #59 does not, and the rubric's tie-break (since all three pass every preferred check identically) fell back to that label plus deliverable size rather than any real judgment of fit, since my `scope.md` fit profile is still a placeholder.
3. I expect claiming #63 to be low-friction: it has no assignee, no prior comments, and the maintainer has been responding to other issues within about a week, so I'd expect a claim comment to get acknowledged reasonably quickly.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
