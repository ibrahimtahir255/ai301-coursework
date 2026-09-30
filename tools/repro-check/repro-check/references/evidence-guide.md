# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->
Every rubric check needs an evidence source. This guide maps the five criterion families to concrete places you can look: on github.com when you are sizing up a live issue by hand, and in the snapshot bundle when you are in eval mode. 

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

| Signal | On github.com | In the eval bundle |  
|---|---|---|
| What the repo requires | the repo's own issue template (`.github/ISSUE_TEMPLATE/`) | the "bug reports" line under Repo facts |
| Candidate's recorded environment | the draft comment/report | the Candidate repro report, usually near the top|

What good looks like: the report states every item the repo's own template asks
for. Some repos name a fixed list (tool version, OS, install method); others state no structured template at all. In that case, "good" means the report still states what tool/version was used and describes the problem and how to reproduce it, since a repo with no template is not a repo with no expectations. Presence is not accuracy: this family checks whether the fields are there, not whether they
match the issue's own stated environment (a version or OS difference belongs to the Behavior-shown or Honesty family, not here).


## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

| Signal | On github.com | In the eval bundle |  
|---|---|---|
| The commands/actions to reproduce | the draft report, wherever it shows commands run | the Candidate repro report: not any specific header name, since candidates structure reports differently (e.g. "Preparation"/"Execution" vs. a single "Steps and observed" block) |

What good looks like: a stranger with no other context could run the exact same commands, in the same order, starting from the same state, and land in the same place. No guessing about a starting state, missing flag, or unstated intermediate action. This family checks followability only, not whether the result matches the issue (that is Behavior shown).


## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

| Signal | On github.com | In the eval bundle |
|---|---|---|
| The issue's own demonstrated failure | the issue body/comments: its command, error text, or panic trace | the Issue section's "Command and actual behavior" block |
| The candidate's demonstrated failure | the draft report's shown output/log | wherever the Candidate repro report shows actual command output |

What good looks like: the artifact the report shows, not what the report claims about it, matches the issue's own artifact: same failure type (a panic is not the same failure as a caught syntax error, even if both come from parsing the same format), triggered by the same or an equivalent input. A report can also show good behavior evidence for an *honest non-match*: full environment, full steps, and
a shown (not asserted) attempt that plainly did not reproduce the issue. What does not count: an assertion of matching behavior with no shown artifact to back it, or an artifact that is quietly a different input/error than the issue describes.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Claims of certainty or success | the draft report's own narrative/analysis language | the report's Analysis/Actual/summary language |
| What the shown artifact actually supports | cross-reference against Behavior shown's artifacts | the report's Analysis/Actual/summary language |

What good looks like: every claim of success, match, or certainty is no stronger than what the shown artifact actually demonstrates. A report that says "could not reproduce" and shows the full honest attempt (environment, steps, actual output of that attempt) is telling the truth, even though it did not reproduce the bug. That is honesty, not failure. A report that asserts a match ("this confirms the reported bug," "exactly the class of failure described") when the shown artifact is a different error, or that claims repeated verification without showing it, is overclaiming — the words say more than the evidence backs, regardless of how confident or polished the writing is.


## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Repo's stated contribution/AI-disclosure policy | `CONTRIBUTING.md`, `AI_POLICY.md`, issue/PR templates | the "contribution policy" line under Repo facts |
| Whether the issue is already claimed | the issue thread: other claim comments, linked/mentioned PRs | the Thread highlights section and any comments shown |
| The candidate's own comment | the draft claim comment | the Candidate claim comment |

What good looks like: the candidate's comment does not contradict a stated repo policy (e.g. a disclosure requirement the comment ignores) and does not proceed as if the issue were unclaimed when the thread already shows a claim or an offered fix the candidate never acknowledges. Silence in the repo facts (no stated policy, no prior claim in the thread) is a pass by default, not a hole. Most repos say nothing, and that is not itself a red flag. This family is about factual accuracy and policy compliance, never about tone, confidence, or formality: a terse or informal comment that is accurate and compliant passes; a polished one that overclaims or ignores an existing claim does not.

## Reading the repo-facts block honestly

The bundle's repo-facts block is captured on a stated date; anything
measured against "current" in the eval bundle means current as of
that capture date, not today. Live mode measures against today.

