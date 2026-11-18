# Issue-scout: a tool that helps you find your first open source issue
 
## Overview
 
Issue-scout is a command-line tool that helps you find your first open source issue. It searches GitHub for issues labelled “good first issue” and grades each one against a written checklist, which I call the rubric, so you don’t have to read hundreds yourself.
 
Many of those labels point at work that is already taken, too big, or in a dead project. The tool began as issue-select, which only graded issues I handed it. When it gained a search stage it became issue-scout, the name I use from here on.
 
It works in three stages: five gh search issues queries, free ranking filters, then paid grading of the top 5 at about $0.20 per issue. An issue is accepted only if every required check passes. I wrote the three files that hold its judgment: rubric.md, the fit profile in scope.md, and search-strategy.md.
 
I ran it on live GitHub twice. The first scan accepted five issues and none were usable. The second rejected all five. The tool now reaches large projects but has not yet produced a usable issue, and my latest fixes are untested.
 
## What happened
 
I wrote the rubric first, with no search, and tested it with the course harness, which grades 20 sample issues against a known answer key. The bar is 18 out of 20. My committed run fell short:
 
```text
agreement: 15/20 scored items  (bar: 18/20: below the bar)
```
 
An earlier full run had scored 18/20. One disagreement stood out: the answer key said to accept a sample issue, but my rubric rejected it because the tracking-issue rule fired. The issue body lists five sub-sections under “Proposed changes,” which I read as one detailed job. I narrowed the rule so it fires only if an issue calls itself a tracking issue, has checkboxes that link to different PRs, or splits work among contributors. Three runs then accepted that issue, but the final full run rejected it again. I concluded the rule “might be borderline and not entirely wrong.”
 
**Scan 1 (Oct 25): five accepted, none usable.** I then ran the full tool, search included (it merges repeat results, called dedup, before ranking), and graded the top 5 results. Two of the five are shown:
 
```text
The five queries returned 500 results. Dedup and the ranking filters cut that to 279, and I graded the top 5. All five are accepted, and all five were surfaced by Query 1 (PyTorch, good first issue, Python).
 
1. BlueprintML#8, Neural Style Transfer in PyTorch. Stars are 14. Last push was today and the latest release was 2026-07-31.
4. topsoilcommons/machine#2, run the PyTorch benchmark and file the JSON. Stars are 0.
```
 
Every accepted issue came from a repo with 0 to 14 stars. The rubric let them through because its popularity check, has-adoption, is only a preferred check: it failed on all five, but preferred checks rank issues and never reject them. The search was also at fault, since “pytorch” matched any small personal repo.
 
**The first fix.** I changed query 1 to search only big ML organisations (pytorch, huggingface, Lightning-AI, pyg-team). I also skipped issues under 7 days old, because brand-new issues always have 0 comments and floated to the top. Finally, I added two rubric rules that fail from-scratch builds and tasks with no code change.
 
**Scan 2 (Nov 1): big projects, five rejections.** The search fix worked: every candidate now came from a project with 2.5k to 35k stars. That was the first result that landed. But all five were rejected. Four had an open pull request (a proposed fix already submitted for review), and two of those also had claims. The fifth, executorch#10819, was rejected because the maintainers were still debating the design. The funnel was 500 results, 137 after the ranking filters, 68 after the cap of 2 issues per repo, then 5 graded.
 
Grading executorch#10819 exposed a gap in my claim rule:
 
```json
{"name": "no-active-claim", "grade": "pass", "evidence": "VarunSai02 'I'd like to work on this' 2026-09-02 is within 60 days, but no maintainer go-ahead; unacknowledged, so passes as written (tension noted)"},
```
 
**The second fix.** The scan also showed a cost problem: open PRs are invisible to the free filters, so they were only caught at the paid grading step. I made two changes:
 
> Change 1 (rubric.md, no-active-claim): My old rule only counted a claim if a maintainer replied. So the scout said executorch#10819 was free, even though someone asked to work on it on 2026-09-02. I changed the rule: any claim in the last 60 days now counts as taken, even with no reply.
>
> Change 2 (search-strategy.md, all queries): I added "-linked:pr" to skip issues that already have a linked PR. Before, these issues only got caught at grading, which costs money. I tested it on query 1: 290 results without it, 175 with it.
 
A linked PR is one GitHub formally ties to an issue, whether open, merged or closed. Change 1 closed a gap but flipped no verdict, since executorch#10819 and diffusers#10076 (which also passed the claim check) were rejected anyway. Change 2 is a result that landed: on query 1, -linked:pr cut 290 results to 175, so 115 fewer issues reached paid grading. Some of those may have been usable, since a closed unmerged PR would have passed the rubric.
 
## Limitations and what's next
 
The scout can’t tell a full fix from a partial one, so any issue with a merged linked PR is an automatic reject. That backfired on VueTorrent #1994, an issue I had picked myself. PR #1999 was merged on 2024-10-28, but it fixed only half of the report, and the maintainer called the reporter’s fuller request a personal choice. The issue is still open.
 
The next step is to have the scout mark such an issue “needs review” instead of rejecting it, and print the PR’s number so I can check it myself. This would be a third outcome beside accept and reject, and it would never count as accepted. I haven’t built this, and I haven’t run a third scan to test any of the Nov 1 changes.
 
