# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/166

**Branch**

fix/72-verify-password-unknown-hash

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (20 packages): `agreement: 13/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in clear-accept)`. My tool rejected all 20 packages, including all 7 clear-accepts.
2. Partial run with `--only` (7 clear-accepts that disagreed, plus canaries pkg-01, pkg-04, pkg-10, calib-01, calib-03): `agreement: 4/10 scored items`. Partial runs don't decide the bar.
3. Full run (20 packages), saved as `eval-run.txt`: `agreement: 19/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

`pkg-02` (Textualize/rich#4208, `Console.save_text` clears the recording when the file write fails). Gold label: `accept`.
 
In my first full run, my rubric decided `reject`, failing only `test-plan-run`. At that point the check required every automated test-plan item to have "its command and real printed output". The plan's test plan said "run pytest", and the package only reported it in a sentence: "`pytest tests/ -q` passes (1462 passed, 12 skipped)". The plan item "a successful save still clears" also had no separate command, because it is checked by the new test in the diff: `assert console.export_text(clear=False) == ""`. My rubric read the sentence as a claim without proof, the same way the class worksheet treated "the full format suite pass" in calib-03.
 
A maintainer would accept pkg-02: the pass/fail counts are specific and checkable, and the second item is a real test in the diff that the pytest run covers. calib-03 only said "pass" with no counts, and its control test was not in the diff. So I changed the check to accept a named command with a specific result, and to count a plan item as tested when a test added in the diff checks it. In my final run (`eval-run.txt`), my rubric decided `accept` for pkg-02, matching gold.

**Check rationale**

From `rubric.md`, check `test-plan-run`:

"Every item in the plan's test plan is reported with its command or steps named and its outcome stated: real output, a result such as pass/fail counts, "passes", or "unchanged", or a specific observed result. A test added in the diff that checks an item counts for that item when the suite that runs it is reported. Any item that failed or was not run is honestly reported with the reason. Fails when a planned item is missing from the evidence, is reported with no command or steps named, or is dismissed ("no further testing seemed necessary")."

It reads this way because my first version was too strict. It required "its command and real printed output" for every automated test, which matched the class worksheet, where a sentence like "tests pass" was never proof. That version failed `test-plan-run` on all 7 clear-accept packages. Looking at the evidence lines, the good PRs did test their changes; they just reported some results as a named command with an outcome instead of pasted output (pkg-02: "passes (1462 passed, 12 skipped)", pkg-16: "`go test ./pkg/minikube/machine/... ./cmd/...` passes"). The not-tested PRs were different: they named no command at all (pkg-04: only "colors work now in paging mode") or skipped testing (pkg-10: "no further testing seemed necessary"). So I rejected "every item needs pasted output" in favour of "every item is named with its outcome", and kept the fail cases for items that are missing, unnamed, or dismissed.

**Trade-offs**

The check now accepts a bare "passes" for a named command, so it gives up catching a PR that names a test suite and claims it passed without really running it. I accept that miss, because the gold labels accept named results like pkg-16's "`go test ./pkg/minikube/machine/... ./cmd/...` passes", and a bare claim that also hides a missing test is still caught by `plan-delivered`.
 
To check that loosening it didn't let bad PRs through, I re-ran canaries with `--only` after the first change: pkg-04 and pkg-10 (not-tested), pkg-01 (standards-wall), and calib-03 all stayed `reject`. The final full run kept `not-tested 4/4` and `standards-wall 2/2`.
 
It also still misses one package I accept it will miss: pkg-19 (gold `accept`) is rejected on `test-plan-run`, because its controls are reported only as "unchanged" with no command or steps named. Loosening further to pass pkg-19 would mean accepting test results with no command at all, which is exactly what makes pkg-04 not-tested.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
