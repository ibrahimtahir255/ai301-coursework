I built a command-line tool called issue-scout that searches GitHub for “good first issue” tasks and checks each one against a written checklist, so a beginner doesn’t have to read hundreds of them. It’s meant to help people find their first open source contribution.

The problem is that many of those labels point at work that is already taken, too big, or in a project nobody maintains.

The first time I ran it on real GitHub, it accepted five issues and none were usable. All five came from tiny projects with 14 stars or fewer. Part of the cause was my search, which matched any small personal repo. The other part was my checklist, which treated popularity as a tiebreaker instead of a requirement. I changed the search to look only at large, established projects, and that worked: every result in the next run came from a project with at least 2,500 stars. But the tool rejected all five of those, because four already had someone working on them and the maintainers were still debating the design of the fifth.

So I added a filter that skips issues GitHub already links to a pull request (someone’s proposed fix). On one search, it cut 290 results to 175, which means fewer issues for the tool to check in detail.

The tool still hasn’t surfaced an issue I could use, and I haven’t tested my latest changes in a full run. But building it showed me how many “good first issues” are already spoken for.

Write-up with the details: https://github.com/ibrahimtahir255/ai301-coursework/blob/main/beat-3-portfolio/technical-writeup.md

#opensource #softwaredevelopment #learning
