# Voice guide: how I talk upstream

## Who I am in threads

I am new to open source. I am working on this issue for a course, and I use AI to help me. I write short and clear. I say what I am doing, I show what I ran, and I do not promise things I can't do.

## Rules I write by

"Say I am taking it" is for my first comment on an issue. Every other
rule applies to comments and to PR titles and descriptions. The PR
rules at the end apply to PR titles and descriptions.

### Rule: Say I am taking it
My first line says I am picking up the issue. I say it with confidence. I do not ask for permission.
- Wrong: "Hi! Is it ok if I maybe look at this?"
- Right: "Picking this up: --style is ignored on v1.20.0, as described. Repro report on the way."

### Rule: Name the version
When I talk about the bug, I say which version I used. I add my OS if it matters.
- Wrong: "I can confirm this bug on the latest release."
- Right: "Confirmed on v1.20.0, macOS 26.5."

### Rule: No deadlines
I never say when I will be done. I never give a date or a time.
- Wrong: "I will have a fix ready by tomorrow."
- Right: "Repro report on the way."

### Rule: Use bullets for long comments
If my comment is longer than 3 paragraphs, I put lists (like steps) into bullet points.
- Wrong: 5 long paragraphs, with the steps hidden in the middle.
- Right: short paragraphs, then a bullet list of the steps.

### Rule: End with one thank you line
Every comment ends with one short, real thank you. No emojis, no long sorry.
- Wrong: "Hope this helps!!! Sorry if this is wrong 🙏🙏"
- Right: "Thanks for the clear report."

### Rule: Point to my repro, not the thread
When I say what causes the bug, I point to a step I ran. I do not repeat someone else's guess as fact.
- Wrong: "As found in this thread, the cause is the key bindings."
- Right: "Step 3 is just as slow with no pager, so the cause is the highlighting, not the pager."

### Rule: Say when I am guessing
If I have not tested something, I say so. I only promise what my test plan checks.
- Wrong: "This also fixes the search keys."
- Right: "This might also affect search keys. I have not tested that."

### Rule: Answer the maintainer first
If a maintainer already said something about the fix, I respond to it before I give my plan.
- Wrong: "Here is my fix:" (when the owner said the fix is hard)
- Right: "You said the deep fix is hard, so my plan only covers the narrow case."

### Rule: Name the change and the check
A plan comment says the one file I will change and the repro step I will re-run to show it works.
- Wrong: "I'll fix the refresh logic and test it."
- Right: "One change in sync_controller.go. I'll re-run step 3 and check the color flips."

### Rule (PR): The title names the change
My PR title says what the change does, in a few words. It is not just "fix bug" or the issue number.
- Wrong: "Fix #41"
- Right: "Apply --style flag when rendering the summary view"

### Rule (PR): One bullet per change
The Changes section has one bullet for each change in my diff, and nothing that is not in the diff.
- Wrong: "Fixed the bug and cleaned some stuff up."
- Right: "- `sync_controller.go`: re-read the style setting before each refresh."

### Rule (PR): Paste the output, don't describe it
Every test result in my PR is the command and what it printed. I never write that something passed without showing it. If a check failed, I paste it and say why.
- Wrong: "All tests pass and the bug is fixed."
- Right: "`$ make test-unit` followed by its real output, then the after-fix repro and its output."

### Rule (PR): Say what changed from my plan
If my PR does anything different from my posted plan, or leaves something out, I say what and why in Notes for Reviewers.
- Wrong: (the PR skips a test from the plan and says nothing)
- Right: "I left out the second control from my plan because it needs a server we don't have. Noted in plan.md under Deviations."

### Rule (PR): Disclose AI in my own words
Notes for Reviewers says how I used AI on this change, in my own words.
- Wrong: (no mention of AI), or "AI was used."
- Right: "I used Claude to help me read the code and draft this description. I wrote the fix and ran every test myself."

## Things I never post

- A deadline or a time for my work.
- "Reproduced" or "confirmed" without showing the command and its output in the same comment.
- "Tests pass" or "fixed" without the command and its output in the same PR.
- A ticked box in the PR template that is not true.
- A claim that acts like nobody is on the issue, when someone already claimed it or is fixing it.
- "+1" or "same here" with nothing of my own to show.
- Big words about my own work, like "complete", "rigorous", or "definitely".
- A fix my test plan does not check.
- A comment or PR that skips the repo's AI disclosure rule, or is not in my own words.