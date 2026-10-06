# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where it lives: The plan's scope/boundary statement and its `## Deviations` section (in `plan.md`, or the bundle's plan-context block), read directly against the diff's changed-file list and hunk contents (`git diff main...HEAD`, or the bundle's diff section). The PR description's claims about what changed also live here, read against the same diff.

What good looks like: Every file the diff touches is either explicitly named in the plan's scope, or explicitly accounted for in a `## Deviations` note explaining why it changed anyway. A description that says "this PR does X" where the diff actually does X-plus-something-unmentioned, or less than X with no note, is silent drift regardless of which direction it runs. An honest deviation note that says "I also had to touch file Y because Z" is not drift — it's drift correctly disclosed, which this family treats as compliant, not as a problem.

## Test evidence (harness category: not-tested)

Where it lives: The PR's test-evidence section (before/after command output), read against the plan's test plan and the original reproduction's steps. The repo's own CI/check results, where visible in the package or on the live PR page, are part of this family too.

What good looks like: A concrete, observable before state and after state — not "tests pass" as a bare assertion, but the actual command run and its actual output, matching the specific behavior the plan's test plan said to check (e.g. "22 passed, 1 xfailed" becoming "23 passed", with the specific previously-failing test now shown passing). If the repo runs its own CI checks, their outcome should be visible and passing, not silently absent from the package.

## Diff quality (harness category: unreviewable)

Where it lives: The unified diff itself and the commit list.

What good looks like: Every hunk in the diff serves the one bounded change the plan describes. No debug print statements left in, no commented-out blocks, no unrelated formatting-only changes to code the plan never named, no drive-by edits to files outside the plan's scope that aren't covered by a deviation note. A reviewer should be able to read the diff and see only the fix — nothing they have to mentally filter out first.

## Standards and comms (harness category: standards-wall)

Where it lives: The repo-facts block's stated PR template sections and contribution policy (including any AI-use disclosure requirement), read against the actual PR description's section-by-section content, and any explicit maintainer direction visible in the thread.

What good looks like: Every section the repo's PR template asks for contains real, specific content — not a copy-pasted placeholder, not a one-word non-answer. If the repo's policy requires AI-assistance disclosure, the description states it plainly, in specific terms (what was used for, not just "AI was used"). A repo with no stated policy passes the disclosure portion by default. (Whether the description's claims actually match the diff is plan fidelity, above — this family is only about whether the repo's own stated asks were honored, not about truthfulness of the match itself.)