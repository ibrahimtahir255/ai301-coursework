# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

<!-- Paste your week-2 section here. -->
I am new to open source. I am working on this issue for a course, and I use AI to help me. I write short and clear. I say what I am doing, I show what I ran, and I do not promise things I can't do.

## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->
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

## Things I never post

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->

- A deadline or a time for my work.
- "Reproduced" or "confirmed" without showing the command and its output in the same comment.
- A claim that acts like nobody is on the issue, when someone already claimed it or is fixing it.
- "+1" or "same here" with nothing of my own to show.
- Big words about my own work, like "complete", "rigorous", or "definitely".
- A fix my test plan does not check.
- A comment that skips the repo's AI disclosure rule, or is not in my own words.