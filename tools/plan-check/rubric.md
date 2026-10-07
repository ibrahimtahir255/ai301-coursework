# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated cause, read against every step (including controls) in the repro evidence. | The plan names a cause, and for every repro step that cause predicts the observed result. Fail if any step's result would not happen if the cause were true. A cause taken from the issue or thread highlights passes only if the repro steps support it; the thread is never evidence on its own. | required |
| targets-cause | The plan's proposed change, read against the cause the repro evidence supports. | The change acts on the cause the repro supports, not on a downstream symptom or on a different component. Fail if the change would leave the repro's failing step unchanged even if implemented perfectly. | required |
| scope | The plan's statement of what it will change and what it won't, read against the repro evidence. | It is one bounded change: the plan identifies where the change goes (a file, function, or module a stranger could find in the repo). An explicit out-of-scope list is not required. Fail if it bundles changes unrelated to the repro'd bug, rewrites or refactors beyond what the fix needs, or its out-of-scope list excludes what the repro evidence points to as the cause. | required |
| executable | The plan's change steps, together with its scope statement. | A stranger with the repo open could start work: the plan names where to change (file, function, or module) and what the change is. Fail only if the change is a goal with no concrete action ("improve handling", "fix the logic") or no findable location at all. Short plans pass if they meet this. | required |
| test | The plan's test plan, read against the repro evidence's steps. | It re-runs the repro step that showed the bug and states the observable result that means the bug is gone. Fail if it only checks that the code change exists, or only that nothing else broke (e.g., "run the full test suite"), without checking the bug's symptom. | required |
| unknowns | The plan and plan comment's claims, read against the repro evidence and thread highlights. | Anything not shown by the repro evidence is stated as an assumption, not as fact, and promised outcomes are ones the test plan would verify. | preferred |
| comment | The plan comment, read against the plan, the thread highlights, and the repo facts (contribution policy, AI policy). | The comment describes the same cause and change as the plan, acknowledges what maintainers already said in the thread, and follows the repo's stated conventions (e.g., an AI disclosure rule, review-bandwidth notes). Fail if it contradicts the plan, ignores a maintainer's position, or breaks a stated repo rule. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept (**ready**) if every required check passes. Reject (**hold**) if any required check fails or is `unclear`; `unclear` counts as fail. Preferred checks never change the verdict; report them as notes. Every grade must quote the line(s) from the package it is based on; a grade with no quote counts as `unclear`.
