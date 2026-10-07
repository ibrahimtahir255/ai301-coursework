# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

Rubric checks covered: diagnosis and targets-cause (Diagnosis and grounding), scope (Scope), executable (Executability), test (Test plan), unknowns (Honesty), comment (Comms). Plans may use any section names or none; find each item by what it says.

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives (package):** The plan's cause is the passage explaining *why* the bug happens: often under Diagnosis, Cause, or Root cause, sometimes in the Summary or the first lines of an unheaded plan. The behavior the cause must explain is in the **Repro evidence** block: its numbered steps, observed results, any control step, and the Expected/Actual lines. Root-cause claims in **Issue** and **Thread highlights** are unverified context, not evidence.

**Where it lives (live):** the draft plan's cause statement; the student's posted repro comment on the issue (steps, outputs, timings); the issue thread for others' claims.

**What good looks like:** The stated cause predicts the observed result of every repro step, including controls and steps where one changed condition flipped the outcome (e.g., color off → fast). The plan's change acts on that same cause. A cause borrowed from the thread is fine only when the repro steps independently support it. Bad: a cause that a repro step contradicts (calib-03: "pager bindings" while the no-pager run is just as slow).

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives (package):** the plan's in/out statements (Scope, In:/Out:, Not in scope) and the file paths named in its change steps (Changes, Change, Approach).

**Where it lives (live):** the same parts of the draft plan; the repo's file tree to confirm the named paths exist.

**What good looks like:** One bounded change: every file to be touched is named by path (e.g., `pkg/gui/controllers/sync_controller.go`), and the out-of-scope list rules out neighbors without ruling out the component the repro points to. Bad: vague locations ("the ignore crate consumer"), several unrelated fixes bundled together, or an out-of-scope list that excludes the real cause (calib-03 excludes syntax highlighting).

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives (package):** the plan's change steps (Changes, Approach, Change:) read together with the scope's file list.

**Where it lives (live):** the draft plan's change steps; the named files/functions in the repo.

**What good looks like:** Each step names a where (file, function, or callback) and a what (the concrete edit), so a stranger with the repo open could start without asking anything. Good: "in the push completion callback in `sync_controller.go`, add the commits context to the post-push refresh scope." Bad: a goal with no action ("fix the matching logic", "improve refresh").

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives (package):** the plan's test passage (Test plan, Test:, Verification), plus any test-adding step in the change steps. Map it against the **Repro evidence** step(s) that showed the bug.

**Where it lives (live):** the draft plan's test section, against the student's posted repro steps.

**What good looks like:** It re-runs the specific failing repro step and names the observable result that means fixed (e.g., "at step 3 the color must flip without leaving the view"; "from `/tmp/rgt`, `two.txt` must not appear"). Extra regression checks are a bonus. Bad: "run the full test suite", or a test that only confirms the code change exists (calib-03's binding-registration smoke test) without checking the symptom.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives (package):** every factual claim in the plan and plan comment, especially side effects and extra fixes ("also fixes search keys"), certainty words ("as identified", "I traced this"), and any risks/unknowns passage. Compare against the **Repro evidence** (what was actually shown) and **Thread highlights** (what maintainers say is unresolved or hard).

**Where it lives (live):** the draft plan and comment; during the build, deviations are recorded as an update to `plan.md` and a follow-up comment on the issue, saying what changed from the plan and why.

**What good looks like:** Claims the repro doesn't show are marked as assumptions or open questions, and promised outcomes are ones the test plan would verify. Good: calib-04 presenting the change as "opt-in... for review" given the owner's note. Bad: stating a thread's guess as fact, or promising fixes nobody tested (calib-03's "brings back... the missing search keys").

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives (package):** the **Candidate plan comment**, read against the plan's cause and change, the maintainer/owner positions in **Thread highlights**, and the **Repo facts** block (bug report template, contribution policy, AI policy, review-bandwidth notes).

**Where it lives (live):** the draft comment; the live issue thread's maintainer replies; the repo's CONTRIBUTING.md, AI_POLICY.md (or equivalent), and issue/PR templates.

**What good looks like:** The comment matches the plan's cause and change, responds to what maintainers already said, and follows stated repo rules. Good: calib-01 keeping it minimal "given the review-bandwidth note in CONTRIBUTING"; calib-04 addressing the owner's "fix is hard" note and the AI-disclosure rule in its own words. Bad: boilerplate that ignores a maintainer's "working as intended", contradicts the plan, or skips a required disclosure.