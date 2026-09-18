# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->
# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer active | Repo-facts block: date of the last commit by a maintainer/owner on the default branch | Last maintainer commit within 120 days | required |
| Maintainer responsive | Comment thread on the issue, or maintainer first-response sample in repo-facts | Unclear only if there is no maintainer first-response sample or comment thread to check at all; otherwise: at least one maintainer reply within 60 days on any recently updated issue, OR a reply on this issue within 45 days | preferred |
| Repo in active use | Repo-facts block: commit frequency over last 90 days, or last push date | 3+ commits in the last 90 days, or last push within 30 days | required |
| Issue not stale | Issue body: creation date and last activity date (last comment) | Last activity within 90 days | preferred |
| Scope fits newcomer | Issue body: description, labels (e.g. "good first issue"), linked files/lines | Labeled as beginner-friendly, OR touches 3 or fewer files, OR describes one specific, narrow, reproducible bug/behavior — but fails regardless of label if the issue body is primarily a list of many linked issues/tasks (an index or "megaissue") rather than one concrete deliverable | required |
| Scope not vague | Issue body: description length and specificity | Issue names a specific bug/behavior, not "improve X" or "refactor Y" generally | preferred |
| Not already claimed or worked | Comment thread: assignment status, comments claiming or showing work on the issue, claim/unassign history | Fails if: (a) a comment shows actual progress already made (code, screenshots, "here's what I have so far"), (b) explicit claim language ("I'll take this," "assigned to me"), (c) GitHub shows an assignee, or (d) the thread shows 3+ prior claim-then-abandon cycles (someone claims, then is unassigned for inactivity, repeatedly) — a pattern suggesting the issue is a known trap even if currently open. Plain expressions of interest ("I'd like to help," "any guidelines?") with no follow-through do NOT count as a claim. | required |
| Not duplicated effort | Comment thread + linked PRs | No open PR already references/closes this issue | required |

## Verdict rule

Accept only if every `required` check passes. Any single `required` check that fails rejects the issue. `unclear` on a required check counts as fail, except where the check itself states otherwise (see "Maintainer responsive," which is preferred anyway and so never affects the verdict). `preferred` checks never flip the verdict; they only break ties when ranking multiple accepted issues (more preferred-passes = higher rank).