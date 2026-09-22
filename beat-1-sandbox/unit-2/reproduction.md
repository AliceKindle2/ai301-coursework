# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[FILL IN: your exact GitHub username, no @ — I don't have this]

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5770428281

Hi! I'd like to investigate this one. Looking at `test_readme_with_all_quality_signals` in `tests/unit/test_readme_scorer.py` — it asserts `word_count > 100` and expects `word_count_category == "comprehensive"`, but the fixture README is only about 51 words, so the test fails with `assert 51 > 100`. I'm going to dig into whether the fixture needs more content or the assertion threshold is the actual issue, and report back what I find.

**Reproduction comment**

[FILL IN: link once you post it — paste the comment's permalink here]

I reproduced this. Running `pytest tests/unit/test_readme_scorer.py -v` shows `test_readme_with_all_quality_signals` marked `xfail` (already tied to this issue via `reason="issue #63: ..."`). Forcing it with `--runxfail` confirms the underlying failure: `assert data["word_count"] > 100` → `assert 51 > 100`, with the scorer correctly logging `word_count=51`, `category=minimal`.

Looking at the fixture, the README text used has all the structural signals (installation, usage, badges, demo link, tech stack) but only ~51 actual prose words — most of its length is markdown syntax (headers, code fences, bullets), which the scorer doesn't count as words. So this looks like a fixture-content issue rather than a scorer bug: the fixture needs more actual prose to legitimately hit the >100 word threshold it's asserting against, or the assertion needs to be reconsidered against what "comprehensive" should require. I'll leave the actual fix decision to the maintainers, happy to help further if useful.

Environment: Python 3.12.10, pytest 9.0.3, commit `f89c06fc3`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

One full run: 19/20 agreement, all category floors passed (`clear-accept 8/8`, `disclosure 1/1`, `no-evidence 4/4`, `unfollowable-comms 2/3`, `wrong-target 4/4`). This matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-19` — gold label: `reject`. My rubric's verdict was `accept`, a false positive, in the `unfollowable-comms` category. [NOTE TO YOU: I have not seen this bundle's actual contents, so I can't honestly write the specific reasoning here — you should open `pkg-19`'s bundle file in your Unit 2 `eval/` materials, read what's actually in the comms/repro report, and describe what your rubric missed. If you'd rather analyze a package your rubric got right, that's equally valid per the assignment ("does not have to be one your rubric got wrong") — pick whichever you can honestly explain.]

**Check rationale**

From `rubric.md`, the "Repo conventions respected" check's pass condition, as currently written:

> If the repo's stated policy requires disclosing AI assistance, the posted comment discloses it; if no such policy exists, this check passes by default.

It reads this way because most repos — including the eval set's packages and the real Path Review repo I worked in — have no AI-disclosure requirement at all. Making the check default-pass in that case means it only actually binds where a real policy exists, rather than penalizing every comment for silence on a topic the repo never raised. I kept this as a `required` check rather than `preferred` because the assignment specifically calls out one disclosure-wall package whose category floor can't be bought back by volume, so I wanted a hard gate here rather than something that could be overridden by other passing checks.

**Trade-offs**

Running my skill live on my actual claim-only draft showed a real limitation of this check design: on a claim-only draft, only one required check ("Repo conventions respected") is actually applicable, since the four repro-report checks report `unclear` and drop out of the verdict rule entirely. Because "Claim comment scope-appropriate" — the check that actually verifies whether the claim names real specifics — is only `preferred`, a claim-only verdict currently rests almost entirely on the default-pass conventions check rather than the thing I actually cared about verifying. I accepted this trade-off since it didn't cost me anything on the 20-package eval (which always grades full packages, not claim-only drafts), but it means my rubric gives weaker signal specifically at the claim-only stage than it does once a full package is assembled.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
