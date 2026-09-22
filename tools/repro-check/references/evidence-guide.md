# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In an eval bundle, the repro report's environment section (usually near the top, before the steps) and the repo-facts block (which states the package/dependency versions the issue targets or the project's stated supported versions). In live mode, the student's draft repro comment's environment section, checked against the repo's own `README.md`, `setup.py`/`package.json`, or CI config for the versions the project actually targets.

What good looks like: The report states the OS, the language/runtime version, and the specific version of the package or dependency involved in the bug — not just "I ran it and it worked/broke," but concrete version numbers. If the environment doesn't match what the issue targets (e.g. issue reports a bug on v2.1 but report used v1.9), that mismatch is called out explicitly by the reporter rather than silently ignored.

## Steps

Where it lives: The repro report's numbered or sequential instructions section, typically following the environment block. In an eval bundle, this is a distinct block of the repro report; in live mode, the corresponding section of the student's draft.

What good looks like: Each step names one concrete, executable action (a command run, a file edited with the exact change, an input given) in order, starting from a clearly stated starting state (e.g. "fresh clone of main," "after running X setup command"). A stranger with no other context could execute the steps as written and land in the same state, without needing to guess a missing action or infer an unstated assumption.

## Behavior shown

Where it lives: The repro report's output/artifact excerpt (error message, log snippet, test failure output, screenshot description) — usually placed right after the steps, showing what happened when the steps were followed. Compare this against the issue's own description of the bug (in the issue context section of the bundle, or the actual GitHub issue body in live mode).

What good looks like: The shown output reproduces the *same* symptom the issue describes — same error message, same failing assertion, same observed incorrect behavior — not a different bug that happens to occur in the same file or area. A pass requires the artifact and the issue's description to describe the same underlying behavior, even if the exact wording differs.

## Honesty

Where it lives: The repro report's stated conclusion, typically at the end ("Reproduced" / "Could not reproduce" / similar), read against the artifacts and steps shown earlier in the same report.

What good looks like: The stated outcome matches what the evidence actually supports. A report that says "could not reproduce" after showing real attempted steps and the actual (non-matching) output obtained is a pass — an honest negative result with evidence behind it. A report that claims "reproduced" without any artifact showing the issue's actual behavior, or where the shown artifact contradicts the claim, is a fail. The bar is alignment between claim and evidence, not whether the bug was successfully triggered.

## Comms

Where it lives: The claim comment text (checked against the issue's own title/description for specificity) and the repro comment text (checked against the repo's stated contribution policy — `CONTRIBUTING.md`, `AI_POLICY.md`, `AGENTS.md`, or similar — found in the repo-facts block of the bundle, or fetched from the repo in live mode).

What good looks like: The claim comment names the issue's actual specifics (the file, the behavior, the failing assertion) rather than a generic "I'll take this." Neither the claim nor the repro comment promises a fix or a delivery date. If the repo's stated policy requires disclosing AI assistance, the posted comment text contains that disclosure plainly; if no such policy exists in the