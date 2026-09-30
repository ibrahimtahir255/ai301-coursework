# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

ibrahimtahir255

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5902000452

Picking this up: verify_password raises UnknownHashError instead of returning False on a malformed stored hash. I see there's already activity on this thread including PR #75 — posting my own claim per the course's Path Review rules. Plan: trace the call into passlib in core/security.py, catch or pre-check for the malformed-hash case so verification fails closed, and confirm the xfail-marked test for H-05 passes once fixed. Repro report on the way.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5902237572

## Repro report

**Environment**

- OS: macOS 26.3.1 (build 25D771280a), arm64
- Python 3.11.0 (the project requires `>=3.11`)
- The repo has no lockfile, so versions were resolved from `pyproject.toml`: passlib 1.7.4 (`passlib[bcrypt]>=1.7.4`), bcrypt 4.3.0 (`>=4.0.1,<5.0.0`), python-jose 3.5.0, pydantic 2.13.5, pydantic-settings 2.15.0, pytest 9.1.1
- Repo at commit `f89c06f`, clean working tree
**Steps** (from the repo root)

```bash
python3 -m venv /tmp/h05-venv
/tmp/h05-venv/bin/python -m pip install -q --upgrade pip
/tmp/h05-venv/bin/python -m pip install -q -e ".[dev]"
 
# 1. Test as written -> "XFAIL", exit 0
/tmp/h05-venv/bin/python -m pytest "tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format" -v -rxX
 
# 2. Same test with xfail disabled -> real traceback, exit 1
/tmp/h05-venv/bin/python -m pytest "tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format" -v --runxfail
 
# 3. Standalone reproduction (no pytest)
/tmp/h05-venv/bin/python -W ignore -c '
from core.security import hash_password, verify_password
print("sanity, valid hash:", verify_password("password", hash_password("password")))
for h in ["not_a_valid_bcrypt_hash", "", "plaintext-password"]:
    try:
        print(repr(h), "->", verify_password("password", h))
    except Exception as e:
        print(repr(h), "->", f"{type(e).__module__}.{type(e).__name__}: {e}")
print()
verify_password("password", "not_a_valid_bcrypt_hash")
'
```

**Actual output**

Step 1 (summary line):

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
======================== 1 xfailed, 2 warnings in 1.81s ========================
```

Step 2 (`--runxfail`), verbatim failure section:

```
>       result = verify_password("password", wrong_hash)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 
tests/unit/test_security.py:227: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
core/security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:2343: in verify
    record = self._get_or_identify_record(hash, scheme, category)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:2031: in _get_or_identify_record
    return self._identify_record(hash, category)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
 
self = <passlib.context._CryptConfig object at 0x118882b50>
hash = 'not_a_valid_bcrypt_hash', category = None, required = True
 
    def identify_record(self, hash, category, required=True):
        ...
        for record in self._get_record_list(category):
            if record.identify(hash):
                return record
        if not required:
            return None
        elif not self.schemes:
            raise KeyError("no crypt algorithms supported")
        else:
>           raise exc.UnknownHashError("hash could not be identified")
E           passlib.exc.UnknownHashError: hash could not be identified
 
/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:1132: UnknownHashError
=========================== short test summary info ============================
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
======================== 1 failed, 2 warnings in 0.97s =========================
```

In that block I replaced passlib's long NOTE/FIXME comment inside `identify_record` with `...`. Everything else is verbatim.

Step 3 (standalone), exit code 1. Python printed the traceback (stderr) before the regular output (stdout):

```
Traceback (most recent call last):
  File "<string>", line 10, in <module>
  File "<repo-path>/core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py", line 2343, in verify
    record = self._get_or_identify_record(hash, scheme, category)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py", line 2031, in _get_or_identify_record
    return self._identify_record(hash, category)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
sanity, valid hash: True
'not_a_valid_bcrypt_hash' -> passlib.exc.UnknownHashError: hash could not be identified
'' -> passlib.exc.UnknownHashError: hash could not be identified
'plaintext-password' -> passlib.exc.UnknownHashError: hash could not be identified
```

A valid bcrypt hash verifies correctly. An empty string or a stored plaintext password raises the same exception, not just the string the test uses.

**Expected:** `verify_password` should fail closed. For any stored hash it can't recognize, it should return `False` instead of raising. The H-05 test's `assert result is False` would then pass, and because the marker is `strict=True`, the `xfail` would need to be removed as part of the fix.

**Unrelated noise:**

- The script also printed `(trapped) error reading bcrypt version ... AttributeError: module 'bcrypt' has no attribute '__about__'`. That's a harmless warning from passlib 1.7.4 running with bcrypt 4.x.
- The pytest runs showed deprecation warnings for `crypt` and Pydantic, plus a Hypothesis warning about its example database.
None of these are related to #72.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (--limit 3): 3/3 agreement — confirmed rubric and evidence guide loaded correctly.
2. First full run: 16/20 agreement, bar not met — categories disclosure 0/1 and unfollowable-comms 1/3 unmatched (pkg-06, pkg-16, pkg-19, pkg-20 disagreed).
3. Diagnosed all four misses individually against their bundles and gold labels; revised behavior-honestly-demonstrated (added platform/version-match clause), promoted policy-honored to required and reworded it (disclosure-by-silence no longer passes), promoted claim-acknowledged to required.
4. Targeted re-run (--only pkg-06,pkg-16,pkg-19,pkg-20 + canaries pkg-01, pkg-05, pkg-09, pkg-12): 8/8 agreement — confirmed all four fixes without flipping canaries.
5. During this round, also discovered and fixed a separate issue: steps-complete was inconsistently grading pkg-05 (immaterial detail treated as a required detail); reworded the check and confirmed with a targeted run (--only pkg-05,pkg-01,pkg-09 + calib-02 as canary): 4/4 agreement.
6. Second full confirming run (--save-run eval-run.txt): 18/20 agreement, bar met, all five categories matched (clear-accept 6/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). Two new disagreements appeared in this run (pkg-03, pkg-07, both failing claim-acknowledged) that were not present in the earlier canary check — logged as a known trade-off, not fixed due to remaining budget constraints.

**Package analysis**

pkg-20 (ghostty-org/ghostty#13604). Gold label: reject. My rubric's verdict: reject, so they agree.

The repo's AI_POLICY.md says all AI usage must be disclosed, including the tool used and how much it helped. The candidate's claim comment doesn't mention AI at all. My first version of the policy-honored check treated that silence as proof no AI was used, so nothing needed to be disclosed. That was wrong. This course's workflow uses AI by default, so silence isn't neutral. It means the repo's disclosure rule wasn't followed. This is also why my first full run missed the whole disclosure category (0 out of 1). I rewrote the check to assume AI assistance by default, so staying silent when disclosure is required now counts as a fail. I also changed the check from preferred to required, so a failure here can actually cause the package to be rejected instead of just being noted. With the new wording, pkg-20 fails policy-honored, and the package is correctly rejected.

**Check rationale**

policy-honored (required): "Pass if the policy does not ban AI-generated contributions outright, AND, assuming the candidate's workflow is AI-assisted (the default for this course), the claim comment or report visibly satisfies anything the policy requires of AI-assisted work (such as stating the tool used and extent of assistance). Pass if the policy states no rule. Fail if there is an outright ban, or if the policy requires disclosure and the comment/report does not contain it, silence is not disclosure."

This check did not always read this way. My first version said a disclosure requirement was only "triggered" if AI use was "claimed or evident" in the comment. That let a package pass just by staying quiet about AI, even on a repo that requires disclosure. My first full eval run showed this was wrong: it missed the one disclosure package in the set completely (0 out of 1 matched). Since this course's workflow is AI-assisted by default, I changed the check to assume AI assistance from the start, so silence no longer defends against a disclosure rule, it fails it. I also moved this check from preferred to required, since a preferred check can never change a verdict on its own, and a disclosure failure needs to be able to hold a package back.

**Trade-offs**

Making claim-acknowledged required fixed pkg-19, where the candidate ignored an open fix PR and promised a guaranteed two day fix. But this same change caused two new misses in my final full run: pkg-03 and pkg-07, both good packages (gold label accept) that my rubric now rejects, both failing claim-acknowledged. I did not catch this in my canary run before the confirming full run, since neither pkg-03 nor pkg-07 was in the small set of packages I re-tested. I'm accepting this as a known gap for now rather than fixing it, since my final run still met the bar at 18 out of 20 with every category matched, and I ran low on eval credits. If I revisit this, I would look at why claim-acknowledged is failing those two specific packages and see if its wording is catching something too broadly.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
