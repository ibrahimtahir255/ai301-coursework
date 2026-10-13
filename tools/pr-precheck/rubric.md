# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| scope-match | The diff's changed files and hunks, read against the plan's Files/scope line and its `## Deviations` notes | Every changed file and hunk is named by the plan (the file or its folder) or explained in a deviation note. Any change outside that fails. | required |
| plan-delivered | The plan's listed changes and tests, read against the diff | Everything the plan says it will change or test appears in the diff, or the description or deviation notes say what was left out and why. | required |
| description-matches-diff | Each claim in the description and checklist, read against the diff | No claim is materially false. Materially false means: the description says something was added or changed that the diff does not contain; it hides or denies a change the diff makes outside the plan (an extra file, an unrelated refactor, a new option); or it claims fidelity ("exactly the plan", "no changes beyond it") that the scope-match or plan-delivered results contradict. Loose wording about how the planned change is organized (a helper function extracted inside the planned change, "one function touched" when a small helper was added beside it) is not material. | required |
| before-after-proof | The test evidence's repro run, read against the plan's repro evidence and the issue's expected behavior | The after-fix repro names the command or steps that were run and shows either real printed output or the specific result observed (named values, messages, or behavior, e.g. "`{ code = 0, stderr = "" }`", "toast 'cannot stash untracked only', no prompt", "searches normally, no error"), and that result is the issue's expected behavior. The before-fix bug is shown by the test evidence, the plan's repro evidence, or the issue. Fails when the repro is missing, names no command or steps, or gives only a vague result ("works", "colors work now", "matches the expected output"). | required |
| test-plan-run | The test evidence, read against the plan's test plan (repro re-run, controls, test files, test suites, smoke checks) | Every item in the plan's test plan is reported with its command or steps named and its outcome stated: real output, a result such as pass/fail counts, "passes", or "unchanged", or a specific observed result. A test added in the diff that checks an item counts for that item when the suite that runs it is reported. Any item that failed or was not run is honestly reported with the reason. Fails when a planned item is missing from the evidence, is reported with no command or steps named, or is dismissed ("no further testing seemed necessary"). | required |
| repo-checks-run | The test evidence and description, read against the checks the repo's PR template or contributing guide asks contributors to run | Every check the repo asks for is reported by name with its outcome (output, counts, "passes", "clean", "no diff"). A failing check reported honestly with its reason passes. Fails when a check the repo asks for is missing entirely or a failure is hidden. | required |
| no-debris | The diff's `+` lines | No debug prints, commented-out code, leftover TODOs, stray files, or formatting-only changes outside the fix. | required |
| template-complete | The description (`pr_draft.md` in live mode), read against the PR template asks in the repo facts or `.github/PULL_REQUEST_TEMPLATE.md` | Every section, checklist item, and entry the template asks for (e.g. a changelog entry) is present with real content (not blank, not a placeholder). No ticked box or checklist claim is contradicted by the diff or evidence. The issue number appears in the title or description (in the exact form the template asks for, such as `Closes #<number>`, if it asks for one). | required |
| disclosure | The description, read against the repo's contribution policy and PR template, and in live mode the course's AI-use disclosure ask | If the repo or course asks for AI-use disclosure, the description includes it. If nothing asks for it, pass. | required |
| clear-title | The PR title, read against the diff | The title names the specific change the diff makes, not just "fix bug" or "update". | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required`
check fails or is `unclear`: an `unclear` grade counts as a fail,
because a claim that cannot be verified from the package is not ready
to submit. `preferred` checks are reported in the summary but never
change the verdict. A shortfall the description honestly discloses,
with its reason, is not a fail for that reason alone: grade the
disclosed shortfall against the check's pass condition, which says
when disclosure is enough.