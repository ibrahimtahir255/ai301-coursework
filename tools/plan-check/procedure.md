# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the **Repro evidence** section first, before anything else. Write down: the environment, each numbered step with its observed result, any control step, and the Expected vs. Actual lines. Mark which steps show the bug and which do not.
2. Note which conditions differ between steps that show the bug and steps that don't (e.g., color on vs. off, cwd `/` vs. `/tmp/x`, pager vs. no pager). These differences are what the plan's cause must explain.
3. Read the **Issue** and **Thread highlights**. Write down every maintainer/owner position (e.g., "working as intended", "fix is hard", "known problem") and every root-cause claim made by anyone. Label each claim **unverified**. Do not use them as evidence for the plan's cause.
4. Read the **Repo facts**. Write down any contribution rule, AI policy, or review-bandwidth note the plan comment must respect.
5. Read the **Candidate plan**, then the **Candidate plan comment**.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

Plans may use different section names or no headings. Find each item by what it says, not its title. For each check, record the item below with a direct quote.

1. **diagnosis:** quote the plan's stated cause. Then build a table: for each repro step (including controls), write the step, its observed result, and yes/no for "if this cause were true, would this result happen?"
2. **targets-cause:** quote the plan's proposed change. Write one line naming the component/behavior it acts on, and one line naming the component/behavior the repro differences (Read order step 2) point to.
3. **scope:** quote the plan's in-scope and out-of-scope statements (if any). Write where the change goes (file, function, or module). List any changes unrelated to the repro'd bug, and anything ruled out that the repro points to as the cause.
4. **executable:** quote each change step. For each one, write the where (file/function) and the what (concrete action), or "missing".
5. **test:** quote the test plan. Write which repro step it re-runs (or "none"), and the observable result it says means fixed (or "none").
6. **unknowns:** list every factual claim in the plan and plan comment that the repro evidence does not show directly (code paths, side effects, extra fixes promised). For each one, write whether it is stated as fact or as an assumption, and whether the test plan would verify it.
7. **comment:** quote the plan comment. Compare it with the notes from Read order steps 3–4 and with the plan's cause and change. Write any mismatch, any ignored maintainer position, and any broken repo rule.

When grading a live issue instead of a package, use references/evidence-guide.md to find where each item lives.


## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Run the checks in this order: diagnosis, targets-cause, scope, executable, test, unknowns, comment. Diagnosis goes first because targets-cause and scope depend on knowing whether the cause is supported.
2. For each check, compare only the evidence recorded for it against that check's pass condition in rubric.md.
3. Grade **pass** if the evidence meets the pass condition. Grade **fail** if it meets a fail condition. Grade **unclear** only if the content the check needs is absent from the package, or the rubric itself marks the case as unclear.
4. Write one reason per grade and include the quote(s) it rests on. A grade with no quote is recorded as unclear.
5. You may grade a check from your recorded evidence without re-reading the package. Re-read the relevant section only if the recorded quote is missing or doesn't settle the pass condition.
6. Grade every check, even after one has already failed. The output reports all of them.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Collect the grades for every required check.
2. If every required check is pass, the verdict is **accept (ready)**.
3. If any required check is fail or unclear, the verdict is **reject (hold)**. Unclear counts as fail.
4. Name the deciding check(s): for hold, every required check that failed or was unclear; for ready, state "all required checks pass".
5. In the output, quote the package line(s) behind each deciding check, alongside its one-line reason, then list every other check's grade and reason.
6. Same grades always produce the same verdict: do not weigh checks against each other or override the rule.
