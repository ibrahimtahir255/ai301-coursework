# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

**Verdict output**


**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

## Summary

All three issues are in the scoped repo (`codepath/pathreview-ai301-fa26-s1`) and **all three pass every required check** — the repo is active (pushed 4 days before today), not archived, has no stated AI-contribution ban, and none of the three issues has an assignee, an open PR, or a blocking claim. Ranked by your fit profile (Python backend background, preference for understanding existing code and reproducing real bugs over test scaffolding):

1. **#72 — `verify_password` raises `UnknownHashError` instead of returning False** (accept). Best fit: a real behavioral bug in `core/security.py` (not test plumbing), closely mirrors your FastAPI/auth experience, carries the maintainer's "good first issue" label, tightly scoped (1–2h), and you'd have to construct your own repro rather than being handed one — good practice for the exact skill you said you want.
2. **#65 — review_service unit tests misconfigure async mocks** (accept). Very strong Python/pytest/TDD match with the clearest repro of the three (one pytest command given verbatim), but the fix lives entirely in test-mock mechanics rather than application logic, and it lacks the "good first issue" label the other two have.
3. **#68 — Keyword search raises `ZeroDivisionError` on empty index** (accept). Good first issue, Python, bounded — but it's a step further from your backend focus (BM25/retrieval library integration), the largest estimated effort (2–4h), and a classmate already posted a full reproduction with traceback today, so less of the "reproduce it yourself" practice is left on the table. (Per the Path Review house rule, their claim doesn't block you from taking it — this is a fit note, not a blocker.)

All three tie on the one preferred check that differs: `has-adoption` fails for all (repo has 1 star, threshold is 1000) — expected for a course repo, and it doesn't affect any verdict.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {"name": "no-assignee", "grade": "pass", "evidence": "assignees: [] via gh issue view"},
      {"name": "no-open-pr", "grade": "pass", "evidence": "gh pr list --state all returns zero PRs for the repo; no cross-referenced PR on issue timeline"},
      {"name": "no-active-claim", "grade": "pass", "evidence": "comments: [] — no claim language present"},
      {"name": "recent-activity", "grade": "pass", "evidence": "repo pushedAt 2026-09-16, 4 days before capture date 2026-09-20 (<30-day threshold)"},
      {"name": "not-archived", "grade": "pass", "evidence": "repo isArchived: false"},
      {"name": "has-adoption", "grade": "fail", "evidence": "repo stargazerCount: 1 (<1000 threshold)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "single-function fix in core/security.py, explicit relevant-files list, 'Estimated effort: 1–2 hours', 'good first issue' label; no tracking/debate/internals/support-question signals"},
      {"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-use policy; no AGENTS.md/AI_POLICY.md in repo root; silence passes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/65",
    "checks": [
      {"name": "no-assignee", "grade": "pass", "evidence": "assignees: [] via gh issue view"},
      {"name": "no-open-pr", "grade": "pass", "evidence": "gh pr list --state all returns zero PRs for the repo; no cross-referenced PR on issue timeline"},
      {"name": "no-active-claim", "grade": "pass", "evidence": "comments: [] — no claim language present"},
      {"name": "recent-activity", "grade": "pass", "evidence": "repo pushedAt 2026-09-16, 4 days before capture date 2026-09-20 (<30-day threshold)"},
      {"name": "not-archived", "grade": "pass", "evidence": "repo isArchived: false"},
      {"name": "has-adoption", "grade": "fail", "evidence": "repo stargazerCount: 1 (<1000 threshold)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "single test-file mock fix with a one-line repro command ('pytest tests/unit/test_review_service.py -q — 13 failed, 6 passed'); not a tracking issue, no design debate, no core-internals statement, not a support question"},
      {"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-use policy; no AGENTS.md/AI_POLICY.md in repo root; silence passes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "no-assignee", "grade": "pass", "evidence": "assignees: [] via gh issue view, despite a claim comment"},
      {"name": "no-open-pr", "grade": "pass", "evidence": "gh pr list --state all returns zero PRs for the repo; the two 'referenced' timeline events are commits on the commenter's own fork, not PRs against this repo"},
      {"name": "no-active-claim", "grade": "pass", "evidence": "comment from yulijasso ('I'd like to take this bug'), authorAssociation NONE, posted 2026-09-20 with no maintainer reply; Path Review house rule says another student's claim doesn't block, and the rubric's own fail trigger (maintainer acknowledgment) never fires since none replied"},
      {"name": "recent-activity", "grade": "pass", "evidence": "repo pushedAt 2026-09-16, 4 days before capture date 2026-09-20 (<30-day threshold)"},
      {"name": "not-archived", "grade": "pass", "evidence": "repo isArchived: false"},
      {"name": "has-adoption", "grade": "fail", "evidence": "repo stargazerCount: 1 (<1000 threshold)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "single-function fix in rag/retriever/keyword_search.py, explicit relevant-files list, 'Estimated effort: 2–4 hours', 'good first issue' label; no tracking/debate/internals/support-question signals"},
      {"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-use policy; no AGENTS.md/AI_POLICY.md in repo root; silence passes"}
    ],
    "verdict": "accept"
  }
]
```


---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `--limit 3` — 2/3
2. `--limit 3` — 3/3
3. full run — 18/20
4. `--only issue-01` — 1/1
5. `--only issue-01` — 1/1
6. `--only issue-01` — 1/1
7. full run with `--save-run eval-run.txt` — **15/20** (the committed run)

**Issue analysis**

`issue-01`. rubric: reject. Gold: accept
scope-fits on original fired the umbrella/tracking disqualifier because the body of the issue lists five sub sections under “Proposed changes”. That is a detailed description of one job, not separately tracked work or links to different PRs. I narrowed passing condition to check whether the description calls itself a tracking issue explicitly or if there are checkboxes that link to different PRs, or if work is split among contributors. Issue-01 has none of this so it should now pass the scope-fit check. I ran the test again on only on issue-01 using `--only issue-01` and they all returned accept. But it rejected again in the final run which suggests that the clause might be borderline and not entirely wrong. 

**Check rationale**

**Check:** `no-active-claim`

> if the comments do not have language that follow the following patterns: "I'll take this", "can I work on this", "working on this" then this check passes + if there are no claim comments within the last 60 days of the capture date then the claim is considered expired and check passes + if the the maintainer acknowledged the claim comment with a reply like "sure, go ahead." then check fails

**Reasoning:** I chose 60 days because the window has to be long enough that a live claim still blocks the issue, and short enough that an abandoned one stops. 30 days felt too short because someone can go quiet for a month and still be working on a fix. Never expiring is worse because a claim with no PR behind it would block the issue forever, even when nobody is on it. Maintainer acknowledgement overrides the 60 day expiry because if the maintainer said "go ahead" and then left the claim standing, no unassignment, no closed PR, I read that as the maintainer still treating the issue as handed over, and unlikely to give it to someone else. So I fail the check regardless of age.

**Trade-offs:** it depends on the assumption that maintainers actively clean up stale assignments. But a lot of them don't and acknowledged claims sit untouched for a long time. This means this clause will sometimes reject issues that are free. `issue-09` is the documented case: gold said accept, my rubric rejected it, and the note names `no-active-claim` as the cause.


---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. The issue's fit to your interests and to the time available.  
   I have already done some work around security and authorization bugs involving bcrypt and JWT so this seemed like a good issue I can handle. Also it is labeled as a `good first issue` with estimated time of 1-2 hours. This leaves room for me to fully understand the reproduction and setup work Unit 2 focuses on.
   
2. What the verdict identified correctly, and what you weighed that the rubric could not.
   The skill got the basic facts right. It confirmed that nobody is assigned to #72, that there are no open pull requests on it, and that nobody has commented to claim it. It also checked that the repo is alive (the last push was 4 days ago) that it isn't archived, and that CONTRIBUTING.md doesn't ban AI-assisted work. It saw that the fix is small and contained: one function in core/security.py plus its test. What my rubric could not do was choose between my three candidates since all three passed every required check. It came down to what I personally would prefer working on. #72 fixes real application code, while #65 only fixes broken test mocks and I would rather work on fixing the program itself.
   
3. The anticipated difficulty in claiming it.
   It should be easy claim since currently there is nobody assigned, no one has commented on it, and the repo has no pull requests. So the issue seems free to claim unless someone claims it before me. 

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
