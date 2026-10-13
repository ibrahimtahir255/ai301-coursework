# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Checks: scope-match, plan-delivered, description-matches-diff.

**Where it lives**

- Eval bundle:
  - What was promised: the **Plan context** section. Its "Files:" line
    lists the files or folders the plan will change; its "Scope" /
    "Not in scope" sentences state the boundary; its "Test plan" lists
    the tests and controls it promised.
  - What was delivered: the **Diff** section. Each file starts with a
    `--- a/<path>` / `+++ b/<path>` header (a new file shows a
    `@@ -0,0` hunk); `+` lines were added, `-` lines removed.
  - What is claimed: the **Description** (its fidelity sentences, like
    "implements the plan exactly", and its checklist), and the
    **Commits** list.
- Live mode:
  - What was promised: `plan.md`, including its `## Deviations`
    section.
  - What was delivered: `git diff main...HEAD` (three dots), run from
    the top folder of the working copy. `git diff main...HEAD --stat`
    lists just the changed files.
  - What is claimed: `pr_draft.md`, in its Summary and Changes
    sections.

**What good looks like**

Every changed file falls inside the plan's named files or folders, or
is explained in a deviation note with a reason. Every change and test
the plan promised appears in the diff, or the description or a
deviation note says it was left out and why. Every claim in the
description is true of the diff: a "Changes" bullet or checklist item
has matching `+` lines, and a "not added" claim has no matching lines.
Loose wording about how the planned change is organized is not drift
(pkg-11: "one function touched" while a small helper was added beside
it, in the planned file).

**What silent drift looks like**

- More than the plan: a file the plan never names is changed, with no
  deviation note (calib-03: a rewrite of `property.js`).
- Less than the plan: a promised test or change is missing and nothing
  says so (calib-03: the all-comments control test).
- False fidelity: the description says "exactly the plan" or lists a
  test that the diff does not contain.

## Test evidence (harness category: not-tested)

Checks: before-after-proof, test-plan-run, repo-checks-run.

**Where it lives**

- Eval bundle: the **Test evidence** section, read against the **Plan
  context**'s test plan and repro evidence, the **Issue**'s input and
  expected output, and the checks named in the **Repo facts** block.
- Live mode: `test_evidence.md`, read against the test plan in
  `plan.md` and the issue's expected behavior. Path Review's PR
  template asks for four checks: `make test-unit`,
  `make test-integration`, `make lint`, and `make typecheck`. The
  before run comes from `main` (or the Unit 2 repro output), and the
  after run from the branch. The Testing section of `pr_draft.md`
  repeats this output.

**What good looks like**

The PR shows it was actually tested and says what happened. The
after-fix repro names the command or steps run and shows real output
or the specific result observed: calib-01 prints `parsed OK`; pkg-13
notes `-- after: { code = 0, stderr = "" }`; pkg-08 lists the steps
and the toast that appears. The before-fix bug is shown in the test
evidence, the plan's repro evidence, or the issue.

Every item in the plan's test plan, and every check the repo asks
for, is reported by name with its outcome: real output, counts
("`pytest tests/ -q` passes (1462 passed, 12 skipped)"), "passes",
"clean", "unchanged", or a specific observed result ("renders
gruvmax-fang unchanged"). A test added in the diff that checks a plan
item counts for it when the suite that runs it is reported. A check
that failed, or stopped as expected (Path Review's
`make test-integration` prints "no tests ran"), is reported as is,
with the reason stated.

In live mode, aim higher than the bar: Path Review's template and
Step 8 ask for the real pasted output of every check, so paste it.

**What not tested looks like**

- No repro at all, or a repro with no command or steps named (pkg-04:
  only "colors work now in paging mode").
- A vague result: "works", "fixed", "matches the expected output".
- A test-plan item or a repo check that the evidence never mentions.
- Testing dismissed (pkg-10: "no further testing seemed necessary").
- An after result that is not the issue's expected behavior.
- A failing check hidden or left out.

## Diff quality (harness category: unreviewable)

Check: no-debris (with scope-match for unrelated files).

**Where it lives**

- Eval bundle: the **Diff** section's `+` lines, and the **Commits**
  list.
- Live mode: the `+` lines of `git diff main...HEAD`, and
  `git log main..HEAD --oneline` for the commits.

**What good looks like**

A reviewer can see the fix and nothing else: every `+` and `-` line
serves the planned change, and every commit message describes part of
that change.

**What unreviewable looks like**

- Debug leftovers: `print(...)`, `console.log(...)`, `debugger`,
  `breakpoint()`.
- Commented-out code or dead code left behind.
- Leftover `TODO` / `FIXME` lines added by the PR.
- Formatting churn: lines changed only in whitespace, quotes, or
  reordering, outside the fix.
- Drive-by edits: refactors or renames unrelated to the issue, even
  inside a planned file.
- Stray files: scratch scripts, local config, or output files.

## Standards and comms (harness category: standards-wall)

Checks: template-complete, disclosure, clear-title.

**Where it lives**

- Eval bundle: the **Repo facts** block lists the PR template's asks
  (sections and checklist items), the contribution policy, and any
  AI-use policy. The **Thread highlights** show any explicit maintainer
  direction. The PR's **Title** and **Description** show whether those
  asks were honored.
- Live mode: Path Review's `.github/PULL_REQUEST_TEMPLATE.md` and
  `docs/CONTRIBUTING.md`; the house rules in `scope.md`; the issue
  thread; and `pr_draft.md`. Path Review's template sections are
  Summary, Issue (`Closes #<number>`), Changes, Testing, Screenshots /
  Demo, and Notes for Reviewers. The course's AI-use disclosure goes in
  Notes for Reviewers.

**What good looks like**

Every section and checklist item the template asks for has real
content, not a blank or a placeholder. Every ticked box is true
according to the diff and the test evidence (the CI box stays
unticked before the PR is opened). The issue number appears in the
title or description, in the form the template asks for if it names
one (Path Review: `Closes #<number>`). An AI-use
disclosure is present wherever the repo or course asks for one. Any
explicit maintainer direction in the thread is followed or answered.
The title names the specific change.

**What a standards wall looks like**

- A template section deleted, left blank, or filled with boilerplate
  ("N/A" with no reason, "see code").
- A ticked box that is not true (for example, "tests added" with no
  test file in the diff).
- The issue number missing from the title and description (pkg-04:
  only the changelog line mentions it), or a missing entry the
  template asks for (e.g. a changelog or whatsnew entry).
- A missing AI-use disclosure where the repo or course asks for one.
- A maintainer's stated direction in the thread ignored.