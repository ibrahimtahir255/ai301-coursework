# Rubric: is this reproduction package ready to post?



## Checks


| Check | Evidence | Pass condition | Weight |
| ----- | -------- | -------------- | ------ |
| env-recorded | The repo-facts "bug reports" line (what the repo asks for), checked against wherever the candidate repro report records its environment, input, and commands | if the repo facts line names specific items, pass if the report contains those items. If the repo facts line states there is no structured template, pass if the report states what tool/version was used and describes both the problem and the steps to reproduce it | preferred |
| steps-complete | wherever the report shows the reproduction steps and the command(s) run | pass if a stranger could re-run the steps and reliably reproduce the same failure — no guessing about anything that would change the outcome (starting state, the specific input or trigger, exact commands/flags). Omitted details that don't affect whether the failure occurs (e.g., unrelated content in a config file, unrelated to the specific field or condition that triggers the bug) don't count against this check | required |
| behavior-honestly-demonstrated | Wherever the report shows the exact input/command used, and wherever it shows that command's actual output, read against the command and error/panic trace in the issue's own "Command and actual behavior" text. | Pass if EITHER (a) the input and command/output shown in the report demonstrate the same failure as the issue's command and error/panic trace, and is not a different error triggered by a different input; OR (b) the report explicitly and plainly states it could not reproduce the issue's behavior, shows the full attempt (environment, steps, and actual output/log of that attempt) as evidence of a genuine try, and does not claim a match it did not get. Fail if the report claims a match that branch (a) does not support, or if branch (b)'s non-reproduction is undocumented (no shown attempt, just an assertion). Additionally, if the issue's behavior is described as specific to a platform, driver, or version (e.g., "only on Windows," or a repo template that requires confirming against latest/main), the match does not hold unless the report's stated environment confirms it was tested under a corresponding platform/driver/version. A report on a substantially different or unconfirmed version/platform does not satisfy branch (a), even if the shown output text matches | required |
| expected-actual-stated | expected and actual lines in the repro report | Pass if the report explicitly states both expected and actual behavior | preferred |
| policy-honored | The repo's contribution-policy line in repo facts (including any AI-use policy quoted there), read against the candidate's claim comment and repro report | Pass if the policy does not ban AI-generated contributions outright, AND, assuming the candidate's workflow is AI-assisted (the default for this course), the claim comment or report visibly satisfies anything the policy requires of AI-assisted work (such as stating the tool used and extent of assistance). Pass if the policy states no rule. Fail if there is an outright ban, or if the policy requires disclosure and the comment/report does not contain it — silence is not disclosure | required |
| claim-acknowledged | The issue's thread highlights, read against the candidate's claim comment | Pass if, when the thread already shows another contributor claiming the issue or a fix in progress, the candidate's comment acknowledges it. Pass if the thread shows no prior claim | required |


## Verdict rule
- accept only if every required check is pass.
- unclear counts as fail.
- Any single required check that is fail or unclear gives reject regardless of preferred results.
- preferred checks are graded and reported but never change the verdict.
- Claim-only drafts (live mode): checks marked not yet applicable: claim-only draft are left out of this rule.