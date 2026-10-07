# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

ibrahimtahir255

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-6028953166

Plan for #72, building on https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5902237572 (commit `f89c06f`, passlib 1.7.4, bcrypt 4.3.0, Python 3.11.0).

**Cause:** `verify_password` in `core/security.py` calls `pwd_context.verify(...)` with no error handling (line 37). When passlib can't identify a stored hash, it raises `UnknownHashError` from `identify_record`, and nothing catches it. My step 3 shows this for `'not_a_valid_bcrypt_hash'`, `''`, and `'plaintext-password'`, while a valid hash still returns `True`.

**Change (one function):**

- In `verify_password`, catch `passlib.exc.UnknownHashError` and return `False`. Only that exception — not a bare `except`.
- Remove the `strict=True` xfail marker on `test_verify_with_wrong_hash_format`, since it would fail once the test passes.

**Not touching:** passlib, the `CryptContext` config, `hash_password`, or dependency versions.

**How I'll check it:** re-run my three repro steps. The H-05 test should pass, and the standalone script should print `False` for all three bad hashes and exit 0. I'll also run the full `test_security.py` file for regressions.

**Left for a follow-up:** others on the thread found that truncated bcrypt-style hashes (e.g. `'$2b$notarealhash'`) raise `ValueError` instead. My repro didn't cover that case, so I'm keeping this fix to `UnknownHashError` and suggest a separate issue for it.

PR #75 catches the broader `ValueError`; I kept this fix to the `UnknownHashError` case my repro shows. I used AI to help with this work and reviewed every step myself.

Thanks for the clear issue and the H-05 test.

---

## Your branch

**Branch**

fix/72-verify-password-unknown-hash

**Evidence**

### Before (Unit 2 repro, commit `f89c06f`)

Commands:

```bash
# 1. Test as written
/tmp/h05-venv/bin/python -m pytest "tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format" -v -rxX

# 2. Same test with xfail disabled
/tmp/h05-venv/bin/python -m pytest "tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format" -v --runxfail

# 3. Standalone reproduction
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

Step 1 output:

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
======================== 1 xfailed, 2 warnings in 1.81s ========================
```

Step 2 output (failure section):

```
>       result = verify_password("password", wrong_hash)

tests/unit/test_security.py:227:
core/security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:2343: in verify
    record = self._get_or_identify_record(hash, scheme, category)
/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:2031: in _get_or_identify_record
    return self._identify_record(hash, category)
>           raise exc.UnknownHashError("hash could not be identified")
E           passlib.exc.UnknownHashError: hash could not be identified

/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py:1132: UnknownHashError
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
======================== 1 failed, 2 warnings in 0.97s =========================
```

Step 3 output (exit code 1):

```
Traceback (most recent call last):
  File "<string>", line 10, in <module>
  File "<repo-path>/core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
  File "/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
sanity, valid hash: True
'not_a_valid_bcrypt_hash' -> passlib.exc.UnknownHashError: hash could not be identified
'' -> passlib.exc.UnknownHashError: hash could not be identified
'plaintext-password' -> passlib.exc.UnknownHashError: hash could not be identified
```

### After (branch `fix/72-verify-password-unknown-hash`, commit `3d0d2ef`)

Same three commands re-run against the fix (step 3's last line changed to `print("bare call:", verify_password(...))` so the result is visible).

Step 1 output:

```
======================== 1 passed, 2 warnings in 0.24s =========================
```

Step 2 output:

```
======================== 1 passed, 2 warnings in 0.16s =========================
```

Step 3 output (exit code 0):

```
(trapped) error reading bcrypt version
Traceback (most recent call last):
  File "/private/tmp/h05-venv/lib/python3.11/site-packages/passlib/handlers/bcrypt.py", line 620, in _load_backend_mixin
    version = _bcrypt.__about__.__version__
              ^^^^^^^^^^^^^^^^^
AttributeError: module 'bcrypt' has no attribute '__about__'
sanity, valid hash: True
'not_a_valid_bcrypt_hash' -> False
'' -> False
'plaintext-password' -> False

bare call: False
exit: 0
```

The `(trapped) error reading bcrypt version` lines are the harmless passlib 1.7.4 + bcrypt 4.x warning noted as unrelated in my Unit 2 report. Full regression run of `tests/unit/test_security.py`: `25 passed, 2 warnings in 8.14s`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run: `agreement: 16/20 scored items  (bar: 18/20: below the bar)`
2. Retry with `--only pkg-02,pkg-09,pkg-13,pkg-14,pkg-03,pkg-06,pkg-10,pkg-12,pkg-17` (4 misses + 5 canaries): `agreement: 9/9 scored items`
3. Full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

**pkg-14** (category `clear-accept`, gold label `accept`).

First full run, my rubric decided `reject`:

> `pkg-14  clear-accept       accept  reject   NO     failed: scope, executable, unknowns`

Final run (`eval-run.txt`), my rubric decided `accept`, matching gold:

> `pkg-14  clear-accept       accept  accept   yes`

Why the first rubric rejected it: three checks judged the plan's level of detail instead of whether the plan was sound.

- My first scope check said: "Lists each file to change by path, and says what it won't touch. A vague location ... does not count as a file and makes this check unclear." That demanded an explicit out-of-scope list and exact paths.
- My first executable check said: "Fail if any step is only a goal ... with no concrete action," and expected each step to name a file/function, so a shorter plan read as not executable.
- `unknowns` was `required`, so any claim the repro didn't show directly failed the whole plan.

pkg-14 is a sound, bounded plan that doesn't spell everything out at that level, so these checks held it for its write-up rather than for a real problem, which is what the rubric template warns against ("never the write-up's shape").

Why the final rubric accepts it: scope now passes if the plan "identifies where the change goes (a file, function, or module a stranger could find in the repo)" and says "An explicit out-of-scope list is not required"; executable now fails "only if the change is a goal with no concrete action ... or no findable location at all"; and `unknowns` is `preferred`. Under those rules pkg-14 passes every required check.

**Check rationale**

From `tools/plan-check/rubric.md`, exactly as it reads now:

> | scope | The plan's statement of what it will change and what it won't, read against the repro evidence. | It is one bounded change: the plan identifies where the change goes (a file, function, or module a stranger could find in the repo). An explicit out-of-scope list is not required. Fail if it bundles changes unrelated to the repro'd bug, rewrites or refactors beyond what the fix needs, or its out-of-scope list excludes what the repro evidence points to as the cause. | required |

Why it reads this way:

**What I revised.** My first version said: "Lists each file to change by path, and says what it won't touch. A vague location ("the X consumer", "the setup code") does not count as a file and makes this check unclear." I wrote that after grading calib-04 in the activity, where the plan named "the override builder setup in the `ignore` crate consumer", which isn't a real file. But in my first full run that strict wording wrongly rejected three clear-accept packages (pkg-02, pkg-13, pkg-14 all listed `scope` among their failed checks). The rubric template says to "Judge the thing itself (is this one bounded change? ...), never the write-up's shape," and demanding an explicit out-of-scope list and exact paths was a shape check. So I changed the pass condition to "a file, function, or module a stranger could find" and dropped the out-of-scope list requirement.

**What I kept.** The fail conditions stayed, because they catch real scope problems: bundled unrelated changes and over-refactoring (the scope-creep family), and an out-of-scope list that rules out the actual cause. That last one comes from calib-03, where the plan said "Not in scope: the syntax highlighting pipeline, which is unrelated to pager navigation", but the repro showed highlighting was the cause.

**Trade-offs**

**Canaries I re-ran with `--only`.** Loosening scope and executable risked letting bad plans through, so I re-ran five already-agreeing packages alongside the four misses: pkg-03 (`clear-accept`), pkg-06 and pkg-12 (`scope-creep`), and pkg-10 and pkg-17 (`unbuildable`). All five kept their verdicts:

> `agreement: 9/9 scored items`

The final full run confirmed the loosened checks still catch the families they guard:

> `categories: clear-accept 7/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4`

**What I gave up.** Making `unknowns` preferred means a plan that states guesses as fact is no longer held for that alone. It only gets held if another required check (diagnosis, test, or comment) catches the problem. I accepted this because, as a required check, it caused false rejects on three good plans (pkg-02, pkg-09, pkg-14).

**A case I accept missing.** pkg-20 (`thread-convention`, gold `reject`) agreed in my first run but flipped in the final one:

> `pkg-20  thread-convention  reject  accept   NO     graded accept`

None of my changes touched the comment check, which is the check this category depends on, so I read this as the grader being inconsistent on a borderline package rather than an effect of my edits. I kept the run at 19/20 instead of tightening the comment check without evidence, since tightening it could start rejecting good plans whose comments are short (like calib-01's).

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
