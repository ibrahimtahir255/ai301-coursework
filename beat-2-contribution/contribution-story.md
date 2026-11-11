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
**Pull Request:** https://github.com/VueTorrent/VueTorrent/pull/3014

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

**Unit 7: Installed the ship-gate with a manifest of VueTorrent's three checks, and used plan-check and the gate to plan, build, and open my PR (2026-11-08 to 2026-11-09)**

I wrote my manifest from VueTorrent's CI file (`npm run test`, `npm run lint`, `npm run build`), and the ship-gate passed on my branch both times, running those checks and then nine pr-precheck checks. At first my hook test showed only the ship-gate's stop message, so I ran my voice guard on its own to confirm it also stopped the command. Plan-check rejected my first plan because no reproduction report was posted on the issue, which conflicts with the assignment's instruction to keep it off, so I quoted my reproduction in plan.md and it accepted. After the first gate PASS I edited my description (version, a Changes list, an untested-RSS note, a thank-you line) and added a Deviations entry, so I ran the gate again; because it could not read the issue thread, I checked the issue for new comments and parallel PRs myself before pushing.

**Unit 8: Wrote a playbook from VueTorrent's real review times, ran the PR monitor on my PR, and agreed with its wait draft (2026-11-10)**

I installed the PR monitor and wrote my playbook from VueTorrent's real data: CONTRIBUTING.md states no wait, and five recent outside-contributor PRs waited 1, 1, 1, 6 and 2 days for a first maintainer response, so my nudge threshold is 7 days. The monitor's state check reported that feedback was in, which made me re-read my PR page and find a finding from CodeRabbit that my earlier note ("no findings") had missed. The full run then drafted "wait, do not reply", and I did not post anything, because no maintainer had commented and the finding is a behavior question that is Larsluph's to decide. The draft got two things wrong. It said it could not tell whether the save path box reacts when code (not a person) sets the path, but my test in the plan had already shown it does not. It also said my PR already lists the bot's case as a known limit, but my PR lists a different case. Because the monitor counts any comment that is not mine, including the bot's, I wrote my quiet-day rule to count only human maintainers and to check the thread myself, and I added to the Maintainer Feedback lines in my story.

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

In `AddTorrentParamsForm.vue`, I will make `onCategoryChanged()` leave the save path alone when the user has typed it and Automatic Torrent Management is off. The form will keep one new piece of state, a ref that records whether the user edited the save path field. The ref is set to true when the field reports a non-empty user change (through its `update:model-value` event), and to false when the user empties the field, so an emptied path is filled in again by the next category change. The ref is checked at the top of the handler. When the path was not edited by the user, the handler behaves exactly as it does today, so picking a category still fills in the category's save path. When the user did edit it, changing the category or clearing it no longer replaces their path.

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
   - listen for `@update:model-value` on the save path `ServerPathField` (lines 187-191) and set the ref to true when the new value is not empty, and to false when it is empty;
   - at the top of `onCategoryChanged()`, return early when `!form.value.use_auto_tmm && savePathEdited.value`.
   Nothing else in the handler changes. I also need to decide when the ref goes back to false (for example when the form is reset after adding a torrent), and I will record that decision below.
4. Add `src/components/Dialogs/AddTorrentParamsForm.spec.ts`, following the existing specs in `src/components/Core/`. It mounts the form with Vuetify and `createTestingPinia({ stubActions: false })`, loads two fake categories, and checks that:
   - a typed path survives a category change with Automatic Torrent Management off;
   - a typed path survives clearing the category;
   - without typing, choosing a category still fills in its save path;
   - with Automatic Torrent Management on, the path is still updated.
   - clearing the path and then changing the category fills in the category's save path (an emptied path counts as not edited).
   I will run the first two on master first and confirm they fail without the fix.
5. Run `npm run test`, `npm run lint`, and `npm run build`. Then repeat the reproduction steps from the Analysis on the branch in mock mode (type /downloads/special, change the category to Music, then clear the category) and expect the path to stay /downloads/special both times.
6. Save the before and after output in `test_evidence.md`, and keep each commit to one change with a message that says what it does.

**Deviations**

- 2026-11-08: Step 2's check is done. Typing in the save path field emits `update:model-value` and a value set from code does not (my first test typed into a hidden input Vuetify adds, and failed until I pointed it at the visible one). I also added a rule: an emptied path counts as not edited. Otherwise a user who clears the box and then changes the category would be left with an empty save path, which is a new behavior nobody asked for. This adds a fifth test in step 4.
- 2026-11-08: Decided when `savePathEdited` resets (plan step 3). It needs no extra code: both dialogs that use the form are rebuilt every time they open, so the ref starts false each time. The cost is the reopen limit described in my PR: a typed path left in the dialog is shown again on reopening, but a category change replaces it.


**Toolkit**

- Tool: plan-check, run through Claude Code on plan.md and plan-comment.md against issue #1994. Claude also helped me draft the Analysis, Proposed Solution, and Implementation Plan, and compared three options for the fix before I chose one.
- What it produced: The first run said reject: every check passed except diagnosis, which was unclear because no reproduction report was posted on the issue. The second run said accept, with all six required checks passing. It also flagged voice-guide breaks in my plan comment and a gap: my reproduction is quoted in prose with no command or output.
- Difficulties: Its advice to post my report on the issue conflicts with the assignment, which says to keep it off, so I did not do that. Claude's first Analysis draft included a claim about the order in which Vue runs the category update and the handler. I had not tested it, so I removed it. The voice-guide breaks plan-check found in my comment are still open, because the comment is not going to be posted.
- What changed: I quoted my reproduction steps and results in plan.md, made plan step 5 name the steps to re-run, replaced "he" with "Larsluph", and cut the untested sentence from the Analysis. I kept my assumption about the maintainer's intended behavior in the plan.

---

## Testing Strategy

**Reproduction, before and after.** On master (commit eba51626, v2.36.1, mock mode, Automatic Torrent Management off), typing `/downloads/special` and then changing the category to Music replaced it with Music's saved path, and clearing the category replaced it with the default path (`/downloads`). On my branch (commit ea052025), the same steps leave `/downloads/special` in place both times. With nothing typed, picking a category still fills in that category's saved path, and with Automatic Torrent Management on, the path still follows the category. The mock backend gives each category a random save path on every page load, so I compared against each category's own path instead of fixed values.

**New tests.** I added `src/components/Dialogs/AddTorrentParamsForm.spec.ts` with five tests. On the unchanged component, the two that cover my fix failed (a typed path was overwritten after a category change and after clearing the category), and the three that guard existing behavior passed. With the fix, all five pass.

**Repo checks.** `npm run test` passes with 32 files and 445 tests (master had 31 files and 440, and the difference is my new spec). `npm run lint` is clean, and `npm run build` succeeds, including the `vue-tsc` type check. I will include the before and after output in my PR description.

**Known limit.** If a user types a path, closes the dialog without adding a torrent, and reopens it, the typed path is still shown but a category change replaces it, as before the fix.

**Toolkit**

- Tool: vitest with @vue/test-utils (the project's own test setup). An AI coding agent in my IDE wrote the spec one step at a time, and I approved each file and each commit. Claude reviewed the agent's proposals and its outputs with me before I approved them.
- What it produced: A five-test spec for the Add Torrent form. Run on the unchanged component, the two tests for my fix failed on their last assertion (the typed path was replaced by the category's path, and then by the default path), and the other three passed. With the fix, all five pass, and the full suite went from 440 to 445 tests.
- Difficulties: My first throwaway check typed into the wrong input, a hidden one that Vuetify adds, so it failed even though the plan was right. `npm run build` also hung in the agent's sandbox, and the mock backend gives categories random save paths, so I could not compare against fixed values.
- What changed: I pointed the tests at the visible input with `input:not([type="hidden"])`, ran the build myself in my own terminal, and compared each result against the category's own path. I also kept the spec uncommitted until the fix was in, so no commit in history has a failing test.

---

## Implementation Notes

**2026-11-08**

I installed the ship-gate and wrote my plan. My first plan-check run said reject, because there was no reproduction report posted on the issue to check my cause against. I did not post one, because the assignment says to keep it off the issue. I quoted my reproduction steps and results in plan.md instead, made the test step name the steps to re-run, and replaced "he" with the maintainer's username. The second run said accept. The maintainer has not answered my question about the intended behavior in manual mode, so I wrote my fix as an assumption in the plan.

Before building, I checked the plan's main assumption, that typing in the save path field emits an event and a value set from code does not. My first test failed because it typed into a hidden input that Vuetify adds, not the real text box. After I pointed it at the visible input, typing emitted the event and code-set values did not, so the plan held. I then added one rule to the plan: an emptied path counts as not edited, so the category fills it in again. That added a fifth test, and I recorded it in the plan's Deviations.

**2026-11-08**

I wrote the spec first and ran it on the unchanged component. The two tests for my fix failed on their last assertion and the other three passed, which is what I expected. The fix is three small changes in `AddTorrentParamsForm.vue`: a `savePathEdited` flag, an early return in `onCategoryChanged()`, and a listener on the save path field. I committed the fix and then the test as two separate commits, so no commit has a failing test. The agent had added a co-author trailer to my first commit message, so I amended the message and made the test commit myself.

While reading the code I found that this form is also used by the RSS rule dialog, so the fix applies there too, with no extra files changed. I also found two limits I am not fixing in this PR. If I type a path, close the dialog without adding, and reopen it, a category change still replaces the typed path. And if I type a path, turn Automatic Torrent Management on and pick a category, then turn it off and pick another, the path set by the code is kept. The mock backend gives each category a random save path on every page load, and `npm run build` hung in the agent's sandbox, so I ran it in my own terminal.

**2026-11-09**

I ran the ship-gate on my branch and it passed. Then I edited my PR description (version and OS, a Changes list, a note that I had not tested the RSS dialog, and a thank-you line) and ran the gate a second time, which also passed. The gate could not read the issue thread, so I checked the issue myself for new comments, assignees, and other PRs before pushing. I pushed the branch and opened PR #3014 through Claude Code. Larsluph and WDaan were requested as reviewers, and CodeRabbit started a review.

**2026-11-10**

I installed the PR monitor and wrote my playbook from VueTorrent's real review times: CONTRIBUTING.md states no wait, and five recent outside-contributor PRs waited 1, 1, 1, 6 and 2 days for a first maintainer response, so I set a 7-day nudge threshold. The monitor reported that feedback was in. When I re-read my PR page, I found a CodeRabbit finding I had missed: if a category fills in the path while Automatic Torrent Management is on, and I then turn it off and change the category, the path is replaced. The issue also says that path should stay, and my fix only protects a path I typed. I did not change the code, because this is the same open question about manual mode that I asked Larsluph, and I did not reply, because no maintainer has commented. The monitor drafted "wait" and I agreed. I also corrected the Maintainer Feedback lines in my story, which had said the bot found nothing.

**Toolkit**

- Tool: Claude, in a chat session. It kept a running list of what happened during the build, and I used it to write the dated entries above.
- What it produced: The entries for the plan-check results, the assumption check, the cleared-field rule, the commits, the RSS dialog finding, and the two known limits.
- Difficulties: The entries were written after the work, so I checked details like commit hashes and test counts against my terminal and test_evidence.md.
- What changed: I edited the entries into my own words. Next time I would add an entry as each step finishes.

---

## Pull Request

**PR Link:** https://github.com/VueTorrent/VueTorrent/pull/3014

**PR Description:** Fixes #1994. In the Add Torrent dialog with Automatic Torrent Management off, a save path the user typed was replaced when they changed or cleared the category. The form now remembers whether the user edited the save path field, so a typed path is kept, and the category still fills in its path when nothing was typed. An emptied path counts as not edited. Behavior with Automatic Torrent Management on is unchanged. The PR has two commits, the fix and five tests. The tests fail on master (the typed path was overwritten) and pass on the branch, and the full suite (445 tests), lint, and build pass. The maintainer has not yet confirmed the intended behavior in manual mode, so the PR says this is my assumption and asks them to redirect me if they want it different. The form is also used by the RSS rule dialog, so the fix applies there too, but I did not test it. Two known limits are noted in the PR.

**Maintainer Feedback:**

- 2026-11-09: none yet. Larsluph and WDaan were requested as reviewers, and a bot (CodeRabbit) started a review with no findings.
- 2026-11-10: No maintainer has responded yet. CodeRabbit, a review bot, posted one finding and a matching Linked Issues warning: if a category sets the path while Automatic Torrent Management is on, and I then turn it off and change the category, the path is replaced. The issue also says that path should stay, and my fix only protects a path I typed.
- 2026-11-10: I did not reply or change the code. My PR already says the manual-mode behavior is my assumption and asks the maintainers to redirect me, so I am waiting for Larsluph or WDaan. My PR monitor drafted "wait" and I agreed.

**Status:** Awaiting review

**Toolkit**

- Tool: The ship-gate, with my manifest (tests, lint, build) and my pr-precheck. I ran it on my branch with my PR title and pr_draft.md, then opened the PR through Claude Code.
- What it produced: PASS both times. It ran my three repo checks and then nine pr-precheck checks, including scope-match, plan-delivered, and before-after-proof. It also listed voice-guide notes and two gaps: it could not read the issue thread, and it could not check for a parallel PR.
- Difficulties: Because it could not read the thread, I checked the issue myself for new comments, linked PRs, and assignees before pushing. The voice-guide notes made me edit my description after the first PASS, so I had to run the gate a second time.
- What changed: I added the version and OS, a Changes section with one bullet per change, a line saying I had not tested the RSS dialog, and a closing thank-you line to pr_draft.md. I also added a Deviations entry to my plan for the reset decision.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned to find where a bug lives in a code base I had not seen: I followed the Add Torrent dialog to `onCategoryChanged()` in `AddTorrentParamsForm.vue` and confirmed the cause by reproducing the bug in the app's mock-data mode. I learned to write component tests with vitest and @vue/test-utils, and to write them first: two of my five tests failed on the unchanged code and all five passed with the fix. I also learned two things about how Vue and Vuetify behave: typing in a field emits `update:model-value` but a value set from code does not, which is the idea my fix rests on, and Vuetify adds a hidden input, so a test has to select the visible one. Finally, I ran the project's own checks (test, lint, build) and kept the fix and its tests in two separate commits.

**Challenges Overcome**

The hardest part was that the maintainer had not said what manual mode should do, and my scout had rejected the issue because of the earlier merged PR #1999. I chose it anyway, wrote my fix as a stated assumption in the plan and in the PR, and asked the maintainers to redirect me. A smaller problem was that my first test typed into a hidden input and failed even though the plan was right; I pointed it at the visible input and the plan held. Plan-check rejected my first plan because no reproduction was posted on the issue, which conflicts with the assignment, so I quoted the reproduction in plan.md instead. 

**What I'd Do Differently Next Time**

I would copy the issue's exact wording into my plan before building. I wrote that the issue wants a typed path kept, but it also says a path set by a category should stay, and I only noticed that when CodeRabbit pointed it out. I would also ask the maintainer's question earlier and wait for an answer before writing code, if the timing allows. I would write each Implementation Notes entry as I finish a step, not afterward, and I would take before-fix screenshots when I reproduce the bug, since I skipped them for lack of time. Last, I would re-read my PR page itself each time instead of relying on an earlier note: my note said the bot found nothing, and it was wrong.

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
