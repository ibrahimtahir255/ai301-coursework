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

In VueTorrent's Add Torrent dialog, with Automatic Torrent Management off, I can type my own save path. If I then change the category, the dialog replaces my path with the category's save path, or with the default path when I clear the category. The path I typed is lost without any warning.


**Expected Behavior**

The issue asks that, with Automatic Torrent Management off, the save path I typed stays the same when I change the category. The maintainer disagrees in part: he says that when a category has its own save path, manual mode assumes I want that path. So it is not decided whether changing the category should overwrite a path I typed. I asked the maintainer in my claim comment, and he has not answered yet.

**Current Behavior**

On v2.36.1 (commit eba5162), using the mock backend: category Movie gives /bin. After I type /downloads/special, switching the category to Music changes the path to /usr/local/src, and clearing the category changes it to /downloads. PR #1999 only fixed the case where a category has an empty save path.


**Affected Components**

- `src/components/Dialogs/AddTorrentParamsForm.vue`: `onCategoryChanged()` (lines 98-105) and the category combobox's `@update:model-value` (line 155). The save path field is only disabled with `:disabled="form.use_auto_tmm"`.
- `src/stores/addTorrents.ts`: holds `addTorrentParams.save_path` and `use_auto_tmm`.
- `src/components/Dialogs/AddTorrentDialog.vue`: sends them as `savepath` and `autoTMM`.
- The preference `use_category_paths_in_manual_mode` (Settings, Downloads) exists, but the add dialog does not read it.

**Toolkit**

- Tool: Claude, in a session linked to my VueTorrent clone. I gave it the issue link and my CLAUDE.local.md, and it read the issue thread and the code (AddTorrentParamsForm.vue, addTorrents.ts, AddTorrentDialog.vue), then drafted the four answers.
- What it produced: A draft of Problem Description, Expected Behavior, Current Behavior, and Affected Components. It confirmed that onCategoryChanged() never reads use_auto_tmm, and it pointed out that the maintainer's view in the thread differs from the reporter's.
- Difficulties: Its page fetch of the issue did not show comment dates or my claim comment, so it could not tell whether the maintainer had answered my question. I checked the thread myself, and he has not replied yet.
- What changed: I edited Claude's draft where it was unclear and checked that it was accurate, direct, and on topic. I reworded Expected Behavior to say plainly that the maintainer's view is still an open question.
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

The bug is in `onCategoryChanged()` in `src/components/Dialogs/AddTorrentParamsForm.vue` (lines 98-105). It is the handler for the category combobox's `@update:model-value` event (line 155), so it runs every time the category changes. It does two things:

- If the new category has a save path, it sets `form.value.save_path` to that path.
- If there is no category (the user cleared it), it sets `form.value.save_path` to the default save path from the preferences.

It never reads `form.value.use_auto_tmm`, and it has no way to tell whether the user typed the current path or whether it was filled in automatically. So in manual mode, any category change overwrites a path the user typed.

The save path field (`ServerPathField`, `v-model="form.save_path"`, lines 187-191) is only disabled when `use_auto_tmm` is on. With it off, the user can type, and nothing protects what they type.

The form's initial values come from `loadAddTorrentOptions()` in `src/stores/addTorrents.ts`, which sets `save_path` to the default and clears the category. `AddTorrentDialog.vue` then sends `save_path` as `savepath` and `use_auto_tmm` as `autoTMM`, so whatever ends up in the field is what qBittorrent receives.

PR #1999 added the `category.savePath.length > 0` check, so a category with an empty save path no longer overwrites the field. That is the only case it fixed. Clearing the category still overwrites the field.

I reproduced this on v2.36.1 (commit eba5162, master) in mock mode with `VITE_USE_MOCK_PROVIDER=true npm run dev`. With Automatic Torrent Management unchecked, category Movie gave /bin. I typed /downloads/special, changed the category to Music, and the path became /usr/local/src. Clearing the category changed it to /downloads. That matches the code: `onCategoryChanged()` sets the path on every category change without checking `use_auto_tmm`.


**Proposed Solution**

In `AddTorrentParamsForm.vue`, I will make `onCategoryChanged()` leave the save path alone when the user has typed it and Automatic Torrent Management is off. The form will keep one new piece of state, a ref that records whether the user edited the save path field. The ref is set when the field reports a user change (through its `update:model-value` event) and checked at the top of the handler. When the path was not edited by the user, the handler behaves exactly as it does today, so picking a category still fills in the category's save path. When the user did edit it, changing the category or clearing it no longer replaces their path.

The maintainer has not yet answered my question about the intended behavior in manual mode, so this is my assumption. I chose it because it fixes what the issue reports, a typed path being lost, and it keeps the behavior Larsluph described, where a category with a save path fills the field. If Larsluph prefers the path to never change in manual mode, the fix is a small step from this one.

What I am deliberately not changing:

- The behavior with Automatic Torrent Management on. The field is disabled and only shows an indicator there, so the handler keeps updating it.
- The `use_category_paths_in_manual_mode` preference. The add dialog does not read it, and what it should do is unclear, so it is out of scope.
- The empty-category-save-path check that PR #1999 added.
- `ServerPathField.vue`, `addTorrents.ts`, `AddTorrentDialog.vue`, and the data sent to qBittorrent.

**Implementation Plan**

1. Create a branch from master, `fix/1994-keep-typed-save-path`.
2. Confirm that typing in `ServerPathField` makes it emit `update:model-value`, and that setting `form.save_path` from code does not. The fix relies on this, so I will check it first, in the browser in mock mode or in the test from step 4. If it is wrong, I will change the plan and record it below.
3. In `src/components/Dialogs/AddTorrentParamsForm.vue`:
   - add a ref, `savePathEdited`, that starts as false;
   - listen for `@update:model-value` on the save path `ServerPathField` (lines 187-191) and set the ref to true;
   - at the top of `onCategoryChanged()`, return early when `!form.value.use_auto_tmm && savePathEdited.value`.
   Nothing else in the handler changes. I also need to decide when the ref goes back to false (for example when the form is reset after adding a torrent), and I will record that decision below.
4. Add `src/components/Dialogs/AddTorrentParamsForm.spec.ts`, following the existing specs in `src/components/Core/`. It mounts the form with Vuetify and `createTestingPinia({ stubActions: false })`, loads two fake categories, and checks that:
   - a typed path survives a category change with Automatic Torrent Management off;
   - a typed path survives clearing the category;
   - without typing, choosing a category still fills in its save path;
   - with Automatic Torrent Management on, the path is still updated.
   I will run the first two on master first and confirm they fail without the fix.
5. Run `npm run test`, `npm run lint`, and `npm run build`. Then repeat the reproduction steps from the Analysis on the branch in mock mode (type /downloads/special, change the category to Music, then clear the category) and expect the path to stay /downloads/special both times.
6. Save the before and after output in `test_evidence.md`, and keep each commit to one change with a message that says what it does.

**Toolkit**

- Tool: plan-check, run through Claude Code on plan.md and plan-comment.md against issue #1994. Claude also helped me draft the Analysis, Proposed Solution, and Implementation Plan, and compared three options for the fix before I chose one.
- What it produced: The first run said reject: every check passed except diagnosis, which was unclear because no reproduction report was posted on the issue. The second run said accept, with all six required checks passing. It also flagged voice-guide breaks in my plan comment and a gap: my reproduction is quoted in prose with no command or output.
- Difficulties: Its advice to post my report on the issue conflicts with the assignment, which says to keep it off, so I did not do that. Claude's first Analysis draft included a claim about the order in which Vue runs the category update and the handler. I had not tested it, so I removed it. The voice-guide breaks plan-check found in my comment are still open, because the comment is not going to be posted.
- What changed: I quoted my reproduction steps and results in plan.md, made plan step 5 name the steps to re-run, replaced "he" with "Larsluph", and cut the untested sentence from the Analysis. I kept my assumption about the maintainer's intended behavior in the plan.

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
