# Procedure: how this tool grades a PR package

## Read order

1. **Live mode only:** read `scope.md` first and apply its stop rules
   (a repo outside scope, or a placeholder on the `Repo:` line, stops
   the run). Then read `voice-guide.md`. In eval mode, skip this step.
2. Read the **plan** before anything in the PR. Live: `plan.md`,
   including any `## Deviations` section. Eval: the bundle's **Plan
   context** section. Write down:
   - every file or folder the plan says it will change (the "Files:"
     line or equivalent),
   - everything the plan says is out of scope (e.g., "no new options",
     "no other statement type"),
   - every item in the plan's test plan (the repro re-run, each
     control, each test suite),
   - every deviation note and the reason it gives.
3. Read the **Issue** and **Thread highlights** (live: the issue
   thread at the URL the student gave). Write down the issue's input
   and its expected behavior.
4. Read the **Repo facts** (live: `.github/PULL_REQUEST_TEMPLATE.md`,
   `docs/CONTRIBUTING.md`, and the course's AI-use disclosure ask).
   Write down every section and checklist item the PR template asks
   for, every check the repo asks contributors to run, and any
   disclosure ask.
5. Read the **Diff** (live: run `git diff main...HEAD`, three dots,
   from the top folder of the working copy). Write down every changed
   file, whether it is new or modified, and one line on what each hunk
   does.
6. Read the **Test evidence** (live: `test_evidence.md`). Write down
   every command or step shown, and whether real printed output or a
   specific stated result follows it.
7. Read the **Title** and **Description** last (live: `pr_draft.md`,
   first line is the title). Write down every claim the description
   and its checklist make, one per line. Label each claim
   **unverified** until a diff line or the test evidence backs it.

Why this order: the plan is read first so the diff is measured against
a fixed list of what was promised. The description is read last so its
claims are checked against what the diff and evidence already showed,
and never used to explain what the diff does.

## Evidence gathering

PRs and plans may use different section names or no headings. Find
each item by what it says, not its title. For each check, record the
items below with a direct quote.

1. **scope-match:** build a table. For each changed file in the diff,
   write the file and `yes`/`no` for "does the plan name this file or
   its folder, or does a deviation note explain it?" For files the
   plan names, also list any hunk that does something unrelated to the
   planned change.
2. **plan-delivered:** build a table. For each change and test the
   plan promises, write where it appears in the diff (quote the file
   or `+` line), or "missing". For each "missing", quote any line in
   the description or a deviation note that says it was left out and
   why.
3. **description-matches-diff:** build a table. For each claim from
   Read order step 7, write the diff line that backs it, or "missing".
   A claim that something was not added ("no options added") is backed
   when nothing in the diff adds it. A fidelity claim ("exactly the
   plan", "no changes beyond it") is false if the scope-match or
   plan-delivered table has any unexplained `no` or "missing". Mark
   each mismatch as **material** (something claimed is not in the
   diff, or a change outside the plan is hidden or denied) or
   **wording** (loose description of how the planned change is
   organized, such as a small helper extracted inside the planned
   change).
4. **before-after-proof:** for the repro after the fix, quote the
   command or steps named (or "none"), and quote either its real
   printed output or the specific result observed (named values,
   messages, or behavior), or write "vague" if the result is only
   "works", "fixed", or "matches". Write whether that result is the
   issue's expected behavior (Read order step 3). For the bug before
   the fix, quote where it is shown: the test evidence, the plan's
   repro evidence, or the issue.
5. **test-plan-run:** for each test-plan item from Read order step 2,
   quote how the evidence reports it: the command or steps named (or
   "none") and the stated outcome (real output, counts, "passes",
   "unchanged", or a specific observed result). If a test added in the
   diff checks the item, quote that `+` line and the suite run that
   covers it. Write "missing" for an item the evidence never mentions,
   and quote any line that dismisses testing ("no further testing
   seemed necessary"). For any item that failed or was not run, quote
   the stated reason (or "none").
6. **repo-checks-run:** for each check the repo asks for (Read order
   step 4), quote how the evidence or description reports it: the
   check's name and its outcome (output, counts, "passes", "clean",
   "no diff"), or "missing". If it failed, quote the stated reason (or
   "none").
7. **no-debris:** scan every `+` line in the diff. Quote each debug
   print (`print`, `console.log`, `debugger`), commented-out code,
   leftover TODO, stray file, or formatting-only change outside the
   fix. Write "none found" if there are none.
8. **template-complete:** for each section, checklist item, and entry
   the template asks for (e.g. a changelog entry), write whether the
   description or diff provides it with real content (not blank, not a
   placeholder). For each ticked box or checklist claim, write whether
   the tables above contradict it. Quote where the issue number
   appears in the title or description, and whether the template asks
   for a specific form (e.g., `Closes #<number>`).
9. **disclosure:** write whether the repo, its template, or (live)
   the course asks for AI-use disclosure. If it does, quote the
   description's disclosure, or write "missing".
10. **clear-title:** quote the title and write one line on what the
    diff actually changes.

When grading a live PR instead of a bundle, use
`references/evidence-guide.md` to find where each item lives.

## Check execution

1. Run the checks in rubric order: scope-match, plan-delivered,
   description-matches-diff, before-after-proof, test-plan-run,
   repo-checks-run, no-debris, template-complete, disclosure,
   clear-title. The scope and delivery checks go first because
   description-matches-diff uses their tables to judge fidelity
   claims.
2. For each check, compare only the evidence recorded for it against
   that check's pass condition in `rubric.md`.
3. Before failing a check for a shortfall, look for an honest
   disclosure of it in the description or a deviation note. Apply the
   check's pass condition to that disclosure: where the condition says
   a disclosed shortfall passes, grade **pass** and quote the
   disclosure.
4. Grade **pass** if the evidence meets the pass condition. Grade
   **fail** if it does not, including when the evidence the check
   needs is absent from the package (no command, no output, no test
   file): absence is a fact, and a claim with no proof fails. Grade
   **unclear** only when the evidence is present but cannot settle the
   condition (e.g., output shown but cut off before the result), and
   name what could not be decided.
5. Write one reason per grade and include the quote(s) it rests on. A
   grade with no quote is recorded as unclear.
6. You may grade a check from your recorded evidence without
   re-reading the package. Re-read the relevant section only if the
   recorded quote is missing or doesn't settle the pass condition.
7. Grade every check, even after one has already failed. The output
   reports all of them.

## Verdict assembly

1. Collect the grades for every required check.
2. If every required check is pass, the verdict is **accept (ready
   to submit)**.
3. If any required check is fail or unclear, the verdict is **reject
   (hold)**. Unclear counts as fail. Preferred checks never change the
   verdict.
4. Name the deciding check: the first required check, in rubric
   order, graded fail or unclear. Quote its evidence first in the
   summary, then list any other failing required checks. For accept,
   state "all required checks pass".
5. Write the summary: one line per check (name, grade, reason with
   its quote), then any procedure gaps, then (live mode only) any
   voice-guide notes.
6. End with the JSON block from `SKILL.md`, with nothing after it.
   Use the bundle id from the bundle's first heading (e.g.,
   `calib-03`) as `item` in eval mode, and the issue URL in live mode.
   List one entry per rubric check, in rubric order, using the
   rubric's check names exactly.
7. Same grades always produce the same verdict: do not weigh checks
   against each other or override the rule.