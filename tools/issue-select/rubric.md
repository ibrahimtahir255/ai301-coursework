# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|no-assignee|this issue: assignees: under Repo facts|an empty or missing "assignees:" line passes|required|
|no-open-pr|linked PRs: under Repo facts, plus PRs mentioned in Comments|no open PR as of the capture date passes + An open linked PR fails but closed unmerged PR passes. A linked PR that has been merged fails and should be considered finished|required|
|no-active-claim|Comments section: claim language, comment date vs capture date|if the comments do not have language that follow the following patterns: "I'll take this", "can I work on this", "working on this" then this check passes +  if there are no claim comments within the last 60 days of the capture date then the claim is considered expired and check passes + if the the maintainer acknowledged the claim comment with a reply  like "sure, go ahead." then check fails|required|
|recent-activity|“Latest release” and "last push to any branch" under Repo facts: |Pass when latest release is lesser than or equal to 365 days from the capture date or the last push is lesser than 30 days from the capture date|required|
|not-archived|"archived:" on the repo line|Pass when archived line is no|required|
|has-adoption|stars on the repo line|Pass when there is at least 1000 stars|preferred|
|scope-fits|the issue body and the comment thread|Passes unless any of these is true: (a) the issue is an umbrella or tracking issue (it calls itself a tracking issue, its checkboxes link to other issues, or it says the work will be split among contributors) listing sub-items meant to be split into separate work; (b) the thread shows the design is still being debated and no maintainer has settled it; (c) a maintainer states the fix touches core internals; (d) the issue is a usage or support question rather than a request for a change. Short is not unscoped: a terse body, a bare checklist, or missing reproduction steps do not fail this check - grade the size of the work requested, not the polish of the write-up|required|
|policy-allows|the "contribution policy" line under Repo facts|Do not Pass when there is an outright ban ("we do not accept AI-generated code". Pass if there is nothing stated or when there are conditions such as Disclosure, personal understanding, testing, and human-review requirements|required|


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
accept if every required check passes; preferred checks never change the verdict, they rank accepted issues; unclear counts as fail.
