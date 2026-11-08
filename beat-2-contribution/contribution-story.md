# Contribution: When adding a new torrent, changing the category should not change the save path if 'Automatic Torrent Management' is disabled

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Ibrahim Tahir
**GitHub Username:** ibrahimtahir255
**Issue:** https://github.com/VueTorrent/VueTorrent/issues/1994
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout, then fixed its search strategy and rubric after two scans and one grading run (2026-10-25 to 2026-11-01)**

I installed issue-scout over my unit 1 rubric and wrote a search strategy from my fit profile: five queries (AI/ML Python first, then Python, Java, and React) and eight ranking rules. My first scan accepted five issues from tiny repos (0–14 stars) because the keyword "pytorch" matched any repo, and after I limited query 1 to big ML organisations, my second scan rejected all five because they already had open PRs or claims that ranking couldn't see. I fixed this by adding `-linked:pr` to my queries (it removed 115 of 290 results before the paid grading step), counting any claim from the last 60 days as taken, skipping issues under 7 days old, and adding `scope-fits` rules against from-scratch builds and no-code tasks. Grading my Issue Selection picks showed the scout accepted Rust and Fortran issues without noticing they didn't fit me, so I added a preferred `language-fit` check, and I let open PRs untouched for 180+ days pass so stale work doesn't block me.

**Unit 6: Built a voice guard and a repo-memory file, then used them to claim and reproduce my issue (2026-11-02 to 2026-11-08)**

I merged my three voice guides into one, added upstream rules for claims, questions and pings, and installed a hook that checks every comment I post through Claude Code against that guide. The hook blocked my wiring test as expected, then passed my claim draft and the real post, and my guard log shows all three. I also wrote a 33-line CLAUDE.local.md for VueTorrent from one scoped orientation run and kept it out of my PR with .git/info/exclude; the run's summary was only a lead, so I confirmed the code myself before trusting it. Nothing broke: I worried my "No deadlines" rule would block my claim's "I'll post what I find once I've reproduced it", so I left the rule alone to test it, and the guard passed the claim anyway.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I found this issue on the Issue Selection site. Most of the Python and Java issues there were already taken, so I graded three picks with my scout: TaskChampion #410 (accepted, moderate), CTSM #2128 (accepted, straightforward), and LandSandBoat #5494 (rejected). TaskChampion needs Rust, which I don't have installed, and CTSM only changes comments, so I wasn't sure it would work for the reproduction step. I looked at a few more issues by hand and skipped the ones where someone was already working on it. Then I graded VueTorrent #1994 with my scout, and the scout rejected it. The only check that failed was no-open-pr, because a merged PR (#1999) is linked to the issue, and my rubric says a merged PR means the issue is already fixed. I chose it anyway. PR #1999 only fixed a small part of the issue: it stops the save path from being overwritten when a category has no save path. The issue is still open and no other PR is linked to it. The scout also said that the open question about what manual mode should do makes this issue ambitious.

This issue fits me because it is a small bug in a Vue and TypeScript web app, and TypeScript is one of my languages. I could also see the bug happen on my own computer using the app's fake-data mode, so I did not need to set up qBittorrent. I hope to learn how to find where a bug lives in a code base I have not seen before, how to make a small fix with a test, and how to work with a maintainer who first said the current behavior might be on purpose. My claim asks him one question about which behavior he wants. As for the scout, my difficulty guesses matched it on all three issues I re-graded. It fell short in a few places. Its "merged PR means fixed" rule rejected an issue that is still open. It also said the old claim on TaskChampion had no go-ahead, but the maintainer had assigned that person and later unassigned them. And language-fit failed on this repo because GitHub calls it "Vue", even though the code is TypeScript. I would change no-open-pr so a merged PR only counts as a fix if it fully solves the issue, and I would add Vue to language-fit.

**Claim comment:** https://github.com/VueTorrent/VueTorrent/issues/1994#issuecomment-6711856229

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric). In Unit 6 I patched the rubric by replacing my scope-fits check with the scope-feasible row and adding a difficulty note (straightforward, moderate, ambitious), then re-graded my three picks and graded this issue.
- What it produced: Two accepted picks with difficulty notes (TaskChampion #410 moderate, CTSM #2128 straightforward), one rejected pick (LandSandBoat #5494, a container issue), and a reject for VueTorrent #1994 because of the merged PR #1999. The patch did not change any of the three verdicts from last week.
- Difficulties: I kept my own fail rules (umbrella issues, usage questions, build-from-scratch requests, run-and-report tasks) instead of pasting the shipped row as is, so my scout is stricter than the patch and can reject issues the patch would accept, for example a small new feature that plugs into existing code. The scout also missed that the TaskChampion claim was assigned and then unassigned, and its merged-PR rule and language-fit check were wrong for #1994.
- What changed: On 2026-11-05 I replaced scope-fits with scope-feasible and moved my old "design still debated" and "core internals" rules into the ambitious note. I would next change no-open-pr so it only fails when the merged PR fully fixes the issue, and add Vue to language-fit.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

I ran this on macOS 26.3.1 with Google Chrome 156.0.8078.73 (arm64), Node v26.7.0 and npm 11.19.0. The project is VueTorrent v2.36.1 at commit eba51626e8a9189e1133dd3ee5ab5438edc222e7 (master), and I cloned my fork and ran `npm ci`. There is no real qBittorrent: I started the app with its built-in fake-data mode using `VITE_USE_MOCK_PROVIDER=true npm run dev` and opened `http://localhost:3000/`. The challenges were small. The public demo site showed a blank white screen, so I ran the demo mode on my own computer instead. The terminal also prints `/backend/ping ECONNREFUSED` errors because no qBittorrent is running, which are harmless. The mock's category save paths are random on each run, so I recorded the paths from one session. `npm test` (440 tests) and `npm run lint` both pass on master before any change.

**Steps to Reproduce**

1. Run `npm ci`, then `VITE_USE_MOCK_PROVIDER=true npm run dev`, and open `http://localhost:3000/`.
2. Click the + button to start adding a torrent.
3. Pick the category Movie. The save path box shows /bin. (The mock's paths are random on each run.)
4. Make sure Automatic Torrent Management is unchecked, so the save path box can be edited.
5. Type /downloads/special in the save path box. It shows /downloads/special.
6. Change the category to Music. Observed result: the save path becomes /usr/local/src, Music's path, and my typed path is lost.
7. Separate case: type /downloads/special again, then clear the category with the x button. Observed result: the save path resets to /downloads and my typed path is lost.

**Reproduction Evidence**

- **Commit showing reproduction:** none. I did not change any code. I reproduced the bug on the upstream master commit eba51626e8a9189e1133dd3ee5ab5438edc222e7.
- **Screenshots/logs:** Values from one session. Category Movie gave /bin. After typing with Automatic Torrent Management unchecked, the path was /downloads/special. After changing the category to Music, it was /usr/local/src. After clearing the category, it was /downloads.

  ```text
  $ git log -1 --format='%H %cd'
  eba51626e8a9189e1133dd3ee5ab5438edc222e7 Sun Nov 1 19:09:20 2026 +0100

  $ VITE_USE_MOCK_PROVIDER=true npm run dev
  > vuetorrent@2.36.1 dev
  > vite
    VITE v8.3.5  ready in 614 ms
    ➜  Local:   http://localhost:3000/
  ```
  
- **My findings:** The bug is real on the current release (v2.36.1), so the report from 2024 (v2.15.0) is not outdated. It happens when Automatic Torrent Management is off and the category has a save path, which is the case that PR #1999 did not fix. Clearing the category also wipes the typed path. The cause is in `onCategoryChanged()` in `src/components/Dialogs/AddTorrentParamsForm.vue` (starts at line 98). It sets the save path from the category, or from the default path when there is no category, and it never reads `use_auto_tmm`. The save path field is only greyed out with `:disabled="form.use_auto_tmm"`. I have not tested a real qBittorrent backend, the case with Automatic Torrent Management checked, or other browsers.

**Toolkit**

- Tool: repro-check, with the real-repo scope file from the Unit 6 setup and my voice guide. I used it to grade my claim draft, and then my claim and my repro report together.
- What it produced: On the claim alone it said accept, with the reproduction checks marked "not yet applicable". On the claim plus my repro report it said accept and every required check passed.
- Difficulties: The first claim check said my draft did not answer the maintainer's view that the current behavior might be on purpose. On the second run, env-recorded failed because the repo's bug template asks for a qBittorrent version and install method, and my report had neither since I used the mock backend. It also said the report was ready to post, but the assignment says to keep the report off the issue.
- What changed: I rewrote the question in my claim so it answers the maintainer directly. In the report I added "qBittorrent: none (mock backend)", the install method, and the terminal output for the commit and the dev server. I did not re-run repro-check after those edits. I kept the report off the issue and will put the proof in my PR description.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
