---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

This tool answers exactly one question: is this PR package ready to submit? A PR package is a candidate pull request — its title, description, commit list, diff, and test evidence — read against two things: the plan it claims to implement (including that plan's recorded deviations) and the issue that plan belongs to. The tool never grades the plan itself, never grades the issue itself, and never answers any question other than ready-to-submit. It does not improvise a verdict from impression; it executes rubric.md's checks via procedure.md's steps, using evidence-guide.md to find each fact.

## Inputs and modes

**Live mode.** Inputs, each named explicitly:
- `plan.md`, including its `## Deviations` section, from the student's working copy.
- The branch's diff: everything the branch changes relative to the repo's default branch, produced by running `git diff main...HEAD` (three dots) from the working copy.
- The student's draft PR title and description (or, once opened, the posted ones).
- The student's test evidence: captured before/after command output, and the repo's own CI check results where visible.
- The issue the plan belongs to, read live from GitHub (thread, labels, state).
A house-chain student substitutes the house plan and the house repro pack for `plan.md` and personal test evidence; every check grades the same things against those instead.

**Eval mode.** A package bundle is the whole world: the plan-context block, the candidate PR's diff/commits/description/test-evidence section, and the repo-facts block (including template asks and stated policy) are all that exists. Nothing is fetched. Every check runs, with the full verdict rule, regardless of package state.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the one repo a PR may target and the house rules governing that repo. If the PR targets any other repository, refuse to grade and say so. If the scope's `Repo:` line still carries an unfilled bracketed placeholder, stop without grading and tell the student to get their cohort's scope file from the instructor — never guess a scope. In eval mode, ignore `scope.md` entirely; the bundle is the whole world regardless of what scope.md says.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md` — the student's own rules for upstream writing, carried forward from week 2. Hold the draft (or posted) PR title and description against those rules, and report any rule the draft breaks in the summary, quoting the rule. The voice guide never changes the verdict on its own unless rubric.md has a check that explicitly reads it. In eval mode, ignore `voice-guide.md` entirely: voice carries no gold labels; universal communication-quality checks live in the rubric itself.

## Component reads

`rubric.md` defines the checks (evidence source, pass condition, weight) and the verdict rule; execute it exactly as written. `references/evidence-guide.md` maps where each evidence family lives in a package or live submission; use it to locate the fact each check names. `procedure.md` is executed as written, stage by stage. If `procedure.md` is silent on a step the tool needs (where to find something, what to do when evidence is missing), report that gap explicitly in the output rather than inventing a step to fill it. If `rubric.md` or `procedure.md` has no real content (only the shipped template comments), refuse to grade and say so: this tool cannot produce a verdict without both.

## Verdict and output

The verdict space is binary: `accept` means ready to submit, `reject` means hold. There is no third verdict and no partial credit. End the reply with the fenced JSON block below, valid and last, with nothing following it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Evidence first: never grade a check without naming the specific fact or quote that decided it; "looks fine" is not evidence. Grade the thing, not the polish: a terse, complete PR can be ready, and a long, confident one can be hiding drift — every check reads the artifact itself against the plan, the issue, and the repo's stated standards, never the write-up's shape or length. The rubric decides, not the run: if a check passes by its literal stated condition but feels wrong, it still passes; a felt wrongness belongs in rubric.md's next revision, not in overriding this run. The procedure decides how, not the run: follow `procedure.md` exactly as written, and report its gaps rather than silently inventing steps around them. Unclear defaults to fail: treat `unclear` as the rubric's verdict rule directs, and where the rule is silent, treat an unverifiable claim as a failing one — a PR whose claim cannot be checked from the package is not ready to submit.