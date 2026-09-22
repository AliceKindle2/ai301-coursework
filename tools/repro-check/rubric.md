# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Repro report's environment section (OS, language/runtime version, package/dependency versions, relevant config) | Report states the OS, runtime/language version, and the specific package version(s) involved in the bug | required |
| Steps complete and followable | Repro report's step-by-step reproduction instructions | Steps are numbered/ordered, each step names a concrete action (command run, file edited, input given), and a stranger could execute them without guessing a missing step | required |
| Behavior matches the issue | Output/artifact excerpt in the repro report, read against the issue's described error or behavior | The observed output/error/behavior in the report is the same behavior the issue describes (same error message, same symptom), not a different or adjacent bug | required |
| Outcome stated honestly | Repro report's stated conclusion (reproduced / did not reproduce) compared against the evidence actually shown | The stated outcome matches what the evidence supports — a "could not reproduce" backed by genuine attempted steps and shown output is a pass; a "reproduced" claim not backed by matching evidence is a fail | required |
| Repo conventions respected | Repo-facts block: any stated contribution/AI-disclosure policy (e.g. CONTRIBUTING.md, AI_POLICY.md) compared against the claim/repro comment text | If the repo's stated policy requires disclosing AI assistance, the posted comment discloses it; if no such policy exists, this check passes by default | required |
| Claim comment scope-appropriate | Claim comment text | Comment names the specific issue/behavior being investigated and does not promise a fix, a timeline, or a completed solution | preferred |
| Report is concise | Repro report overall length and signal-to-noise | Report conveys environment, steps, and outcome without unrelated padding | preferred |

## Verdict rule

Accept (ready to post) only if every `required` check passes. Any single `required` check that fails, or is `unclear`, holds the package (reject) — treat `unclear` as fail, since unverifiable proof is not proof ready to post upstream. `preferred` checks never change the verdict; they only inform overall quality notes in the summary.