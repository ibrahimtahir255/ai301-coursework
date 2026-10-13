---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

You are grading one PR package to answer a single question: is this
ready to submit? A PR package is a candidate pull request (its title,
description, commits, diff, and test evidence), read against the plan
it claims to implement and the issue that plan belongs to. Answer only
this question, about only this one package. Do not grade the plan
itself, the issue, or any other PR, and do not answer from gut feel:
answer by executing `procedure.md`, which applies the checks in
`rubric.md` to evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->


Run in exactly one of two modes.

**Live mode**: the student's own PR, checked before it is opened. Read
these inputs, and only these:

- **The plan**: `plan.md` in the working directory, including any
  `## Deviations` section. Deviation notes are part of the plan and
  are graded like the rest of it.
- **The diff**: every committed change the branch makes compared with
  `main`. Produce it by running `git diff main...HEAD` (three dots)
  from the top folder of the working copy. Uncommitted changes are not
  part of the PR; do not read them.
- **The title and description**: `pr_draft.md`. The first line is the
  PR title; everything below it is the description, written into the
  repo's PR template.
- **The test evidence**: `test_evidence.md`, holding the before and
  after repro output and the output of the checks the PR template
  asks for.
- **The issue**: the issue URL the student gives. Read its thread live
  (via `gh`, the GitHub API, or the web).
- **The repo's standards**: the PR template at
  `.github/PULL_REQUEST_TEMPLATE.md` and the contribution policy at
  `docs/CONTRIBUTING.md`, read from the scoped repo.

A student on the house chain reads the house plan and the house repro
pack in place of their own plan and repro evidence; the same checks
grade the same things there. Do not read any other file in the working
directory (such as `comment.md`): the package is what these inputs
contain, not everything on disk.

**Eval mode**: the input is one package bundle, a markdown file from
`eval/packages/` containing repo facts, the issue, thread highlights,
the plan context, and the candidate PR (title, description, commits,
diff, and test evidence). The bundle is the whole world: use only its
text as evidence, and fetch nothing. Always grade a complete package in
eval mode: run every check and apply the full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->


In live mode, read `scope.md` in this skill directory before anything
else. It names the one repo the student's PR may target and the house
rules that apply there (branch naming, one PR per issue, the template
always used). Apply those house rules when reading the evidence: they
are part of the bar this PR must meet.

Refuse to grade a PR whose issue or target repo is outside the repo
named on the scope's `Repo:` line; say which repo is in scope and
stop. If the `Repo:` line still carries an unfilled placeholder, stop
without grading and tell the student to fill the `Repo:` line in
`scope.md` with their section's Path Review repo. Never guess a scope.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->



In live mode, after reading `scope.md`, read `voice-guide.md`: the
student's own rules for how they write upstream, with wrong and right
examples. Hold the outgoing PR text, the title and the description in
`pr_draft.md`, against those rules. In the summary, report each rule
the draft breaks, quoting the rule and the line that breaks it.

The voice guide never changes the verdict on its own unless the rubric
has a check that reads it. A PR can break a voice rule and still be
ready to submit; the voice notes are advice for the student, not a
grade.

In eval mode, ignore `voice-guide.md` entirely: voice is personal and
carries no gold labels. Universal communication-quality checks live in
the rubric.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read the components in this skill directory and use each for its job:

- **`rubric.md` is the brain.** It defines a table of checks (each row
  names the check, the evidence to gather, the pass condition, and its
  weight) and a verdict rule. `required` checks gate the verdict;
  `preferred` checks never change it. The verdict rule says how check
  grades combine into `accept` or `reject`, including what an
  `unclear` grade does.
- **`references/evidence-guide.md` is the map.** It says where each
  kind of evidence lives in a PR package, in an eval bundle and in a
  live PR, and what good looks like there.
- **`procedure.md` is the hands.** Execute it as written: it decides
  the read order, how each kind of evidence is gathered, how each check
  runs against that evidence, and how check grades become the verdict.

Follow the procedure exactly. Where it is silent on a step, do not
invent one: note the gap in the summary and continue with what the
procedure does say. A procedure gap is feedback the student needs.

If `rubric.md` has no checks written, or `procedure.md` has no steps
written, stop without grading and say which file is empty. This skill
cannot grade without a rubric and a procedure, by design: a tool that
invents its own checks gives verdicts that look like judgment but are
noise. Comments inside a file do not count as content; only written
text does.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict space is binary: `accept` means ready to submit, and
`reject` means hold. There is no third verdict, no "accept with
reservations," and no score; reservations belong in a check's evidence
line, not in the verdict.

Before the JSON block, you may show a short readable summary: one line
per check with its grade and evidence, then any procedure gaps, then
(live mode only) any voice-guide notes. Then end your reply with the
fenced JSON block below. It must be present, valid, and last, with
nothing after it: the eval harness parses the last fenced JSON block in
your output.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- **Evidence first.** Never grade a check without naming the fact or
  quote that decided it: a diff line, a line of real command output, or
  a sentence from the plan or description. "Looks fine" is not
  evidence. A sentence claiming something passed is not proof that it
  passed, and neither is a note after `#`; only the command and its
  printed output are.
- **Grade the thing, not the polish.** A short, complete PR can be
  ready, and a well-written, confident one can be hiding drift. Read
  the diff, the evidence, and the description against the plan, the
  issue, and the repo's stated standards, never the formatting.
- **The rubric decides, not you.** If a check passes by its stated
  pass condition but feels wrong, it still passes. Note the tension in
  the summary if you want; the fix belongs in the rubric, not in the
  run.
- **The procedure decides how, not you.** Follow `procedure.md` as
  written, and report its gaps instead of filling them in.
- **Unclear defaults to fail.** Treat `unclear` as the rubric's verdict
  rule directs. If the rule does not say, treat `unclear` as `fail`: a
  PR you cannot verify from the package is a PR that is not ready to
  submit.