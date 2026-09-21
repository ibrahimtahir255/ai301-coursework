# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s1` <!-- paste your section's repo from the Unit 1 Check-In page -->

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

<!-- YOU write this part: a few sentences about you. What languages and
tools you have actually used, what you want to get better at, anything
you want to avoid. The skill uses this only to RANK the issues your
rubric accepts, never to change a verdict: fit cannot rescue an issue
your rubric rejects, and cannot sink one it accepts. -->

I'm a CS graduate whose hands-on work is mostly Python backends: FastAPI
services with typed endpoints, pytest and test-driven development, plus
Pandas/NumPy and PyTorch from research work. I've also built a
Next.js/TypeScript site, deployed to AWS with Terraform and GitHub
Actions, and I use Git daily.

Python is the language I'd back myself in under time pressure, so rank
Python issues first. I can work in TypeScript but I'm slower there.

Most of what I've built has been greenfield — I wrote the code and knew
where everything was. What I want from this term is the opposite:
reading a large codebase I didn't write and finding the few files that
matter, reproducing someone else's bug reliably before touching it, and
working through review with maintainers I don't know. The closest I've
come is integrating a teammate's feature branch, where I resolved the
merge conflicts and caught two silent regressions it had introduced.

So I'd rather have an issue that requires understanding existing code
than one where I add something new alongside it. A bug with a clear
reproduction path suits me better than open-ended feature work. I have
no hard exclusions on domain or setup.
