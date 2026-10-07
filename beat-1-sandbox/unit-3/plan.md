# Plan: `verify_password` fails closed on malformed stored hashes (#72)

## Diagnosis

`verify_password` in `core/security.py` passes the stored hash straight to passlib with no error handling (line 37):

```python
return bool(pwd_context.verify(plain_password, hashed_password))
```

When passlib can't identify the hash's scheme, `CryptContext.verify` raises `passlib.exc.UnknownHashError` instead of returning False. Nothing in `verify_password` catches it, so the exception escapes to the caller.

Evidence from my repro (commit `f89c06f`, passlib 1.7.4, bcrypt 4.3.0, Python 3.11.0):

- Step 3, valid hash: `sanity, valid hash: True` — verification works when passlib can identify the hash.
- Step 3, unrecognizable hashes: `'not_a_valid_bcrypt_hash'`, `''`, and `'plaintext-password'` each give `passlib.exc.UnknownHashError: hash could not be identified`.
- Step 2 traceback: the exception is raised at `passlib/context.py:1132 in identify_record` (`raise exc.UnknownHashError("hash could not be identified")`) and passes up through `core/security.py:37 in verify_password` uncaught.

The cause explains every step: valid hashes are identified and verify normally; every hash passlib can't identify raises from `identify_record` and is not caught in our code.

## Scope

**In scope:** one change to `verify_password` in `core/security.py`, plus removing the now-obsolete `xfail` marker in `tests/unit/test_security.py`.

**Not in scope:**

- passlib itself, or the `CryptContext` configuration (schemes, rounds).
- `hash_password` or any other function in `core/security.py`.
- The passlib/bcrypt `__about__` version warning and the deprecation warnings seen during the repro — unrelated to #72.
- Upgrading passlib or bcrypt.
- Bcrypt-shaped but truncated hashes (e.g. `'$2b$notarealhash'`). Others on the thread report these raise `ValueError`, not `UnknownHashError`. My repro didn't cover them, so they belong in a separate follow-up issue rather than this fix.

## Files I'll touch

- `core/security.py` — `verify_password`
- `tests/unit/test_security.py` — `TestSecurity::test_verify_with_wrong_hash_format` (remove the `xfail` marker)

## Approach

1. In `core/security.py`, import `UnknownHashError` from `passlib.exc`.
2. In `verify_password`, wrap the `pwd_context.verify(...)` call in `try/except UnknownHashError` and return `False` in the `except` branch. Catch only this exception — not a bare `except Exception` — so unrelated errors still surface.
3. In `tests/unit/test_security.py`, remove the `@pytest.mark.xfail(..., strict=True)` marker from `test_verify_with_wrong_hash_format`. Because it's `strict=True`, leaving it would make the test fail once the fix makes it pass.

## Test plan

Re-run my Unit 2 repro steps after the change:

1. **Step 1 (test as written, marker removed):**
   `python -m pytest "tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format" -v`
   Expect: `PASSED` (was `XFAIL`).
2. **Step 2 (with `--runxfail`):** same command with `--runxfail` added.
   Expect: `PASSED`, no `UnknownHashError` traceback (was `FAILED`, exit 1).
3. **Step 3 (standalone script):** expect this output, with exit code 0:

```
   sanity, valid hash: True
   'not_a_valid_bcrypt_hash' -> False
   '' -> False
   'plaintext-password' -> False
```

   and the final bare `verify_password("password", "not_a_valid_bcrypt_hash")` call no longer raises.
4. **Regression check:** `python -m pytest tests/unit/test_security.py -v` — all other security tests still pass, including correct/incorrect password checks on valid hashes.

## Risks and unknowns

- **Truncated bcrypt-style hashes still raise:** per the thread, these raise `ValueError`, which this fix doesn't catch. I'm keeping the fix to the case my repro proved and flagging the rest as a follow-up.
- **`None` as a stored hash:** not tested in my repro; passlib may raise `TypeError`. Out of scope unless the build shows the existing tests need it.
- **PR #75:** touches the same two files but catches the broader `ValueError`. My fix stays narrow to the `UnknownHashError` case my repro proved.
- **Silencing errors:** returning False hides the fact that a stored hash is corrupt. Logging it is a reasonable follow-up but is not part of this fix.

## Deviations

No deviations. The build followed the plan: I added one try/except UnknownHashError in verify_password that returns False, and removed the strict xfail marker from test_verify_with_wrong_hash_format. Nothing else changed. All 25 tests in test_security.py pass, including the H-05 test that was XFAIL before.