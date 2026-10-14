# Plan: redact parenthesized US phone numbers (issue #53)

## Diagnosis

The phone_us pattern is \b(?:\+?1[-.]?)?\(?([0-9]{3})\)?[-.]?([0-9]{3})[-.]?([0-9]{4})\b. 
It fails (555) 123-4567 twice over: the separator class after the area code is [-.]? with no space, 
so the match dies at the space after ); and the leading \b can never precede (, so the match would 
start at 555 and leave the opening paren behind anyway. Because the pattern requires 10 digits in 
3-3-4 form, the trailing 123-4567 cannot partially match either -- consistent with the quoted repro issue above, 
where the entire parenthesized form survives scrub() and detect() returns [].

Repro evidence — quoted verbatim from my repro comment on issue #53:

````text 
Reproduced on my end.

## Environment

- OS: Windows 11 25H2 (build 26200.9550)
- Python 3.14.5 — repo minimum is 3.11 (`requires-python = ">=3.11"` in pyproject.toml); calling out the difference, the bug is pattern-based, not version-specific
- pytest 9.1.1
- Repo: fork's main at commit f89c06f
- Backing services (Docker/Postgres/Redis) not started — this is the pure-Python scrubber unit path with no DB/API dependency. Flagging the deviation from SETUP.md in case it matters for re-runs.

Setup commands as run:

```
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -e .
pip install pytest pytest-asyncio
```
## Original issue

Per the issue body: the phone pattern matches dashed formats like `555-123-4567` but not the parenthesized `(555) 123-4567`, so that format passes through `scrub()` unredacted and `detect()` reports no PII for it. 

Expected: `scrub()` redacts `(555) 123-4567` the same way it redacts `555-123-4567`, and `detect()` reports it.

## Steps

1. Saved the issue's snippet verbatim as repro.py:

```python
from safety.pii_scrubber import PIIScrubber
s = PIIScrubber()
print(s.scrub('Call me at (555) 123-4567 or 555-123-4567'))
print(s.detect('Call me at (555) 123-4567'))
```
2. Ran twice: `python repro.py`

3. Ran the four related tests:

```
pytest tests/unit/test_pii_scrubber.py -k "us_phone_number_redaction or us_phone_formats or detect_phone_pii or phone_at_start_of_text" -v
```

## Observed 

Ran the command 'python repro.py' (identical across two runs):

```
Call me at (555) 123-4567 or [REDACTED]
2026-09-30 02:33:36 [info    ] pii_detected count=0 types=0
[]
```
The parenthesized format survives scrub() while the dashed format is redacted; detect() returns [].

pytest:

```
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction XFAIL [ 25%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats XFAIL [ 50%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii XFAIL [ 75%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text XFAIL [100%]


============= 21 deselected, 4 xfailed in 0.34s ====
```

The four tests carry xfail(strict=True) markers per CONTRIBUTING.md (seeded bugs stay green this way); all four xfail as expected.

## Outcome

Reproduced: the parenthesized format passes through `scrub()` unredacted and `detect()` reports nothing for it, in this environment, on current main — matching the issue's observed behavior exactly.
 
## Scope

In: the US phone-number regex in `safety/pii_scrubber.py`, plus the
`xfail(strict=True)` markers on the four phone tests in
`tests/unit/test_pii_scrubber.py`. Out: every other PII pattern, the
redaction/replacement mechanism, `detect()`'s structure, and every
other test and marker in the test file.

## Files

- `safety/pii_scrubber.py` — the phone-number pattern only.
- `tests/unit/test_pii_scrubber.py` — remove the `xfail(strict=True)`
  markers from the four phone tests only (per CONTRIBUTING.md's
  convention; a fixed bug's marker comes out).
```
```
## Approach

1. Read the current phone pattern and confirm exactly why `(555) ` is not matched.

2. Change the leading \b to (?<!\w) so the match can start at (, and the first 
separator class [-.]? to [-. ]? so the space after ) is consumable. One line in 
`safety/pii_scrubber.py`.

3. Read the four phone tests first; if test_us_phone_formats asserts formats 
beyond the parenthesized one, widen the separator classes to match the tests 
exactly and note the choice.

4. Remove the xfail(strict=True) markers from the four phone tests (per CONTRIBUTING.md's convention).
```
## Test plan

Unit 2 repro steps re-run — the exact snippet from the issue run before
and after. Before: `'Call me at (555) 123-4567 or [REDACTED]'`.
After: `'Call me at [REDACTED] or [REDACTED]'`.

```
Automated: `pytest tests/unit/test_pii_scrubber.py -k phone`. Before the
fix, `test_us_phone_number_redaction`, `test_us_phone_formats`,
`test_detect_phone_pii`, and `test_phone_at_start_of_text` fail. After:
all four pass and the full test file stays green.
```

## Risks and unknowns

- Resolved by reading the code: scrub() and detect() share the single 
PII_PATTERNS dict, so the one-line pattern change covers both methods.

- Accepted consequence: the space in the first separator also matches 
space-separated forms like 555 123-4567. Standard US format, kept deliberately; 
will mention in the PR.

- The marker removal slightly widens scope to the test file; bounded to four markers.
````

## Deviations

```
The build followed the plan; step 3's conditional widening triggered.
`test_us_phone_formats` asserts `+1 555 123 4567`, so both separator
classes after the area code became `[-. ]?`; no wider. The country-code
group's own separator stayed `[-.]?`, so that format scrubs to
`+1 [REDACTED]` — deliberate boundary.

Marker scope, corrected at pre-check: the first version of this branch
also removed the xfail(strict=True) marker on test_mixed_pii_and_text
(it cites issue #53). That test fails because of the pre-existing
case-insensitive street_address pattern ("Python appl" matching the
`Pl` alternative in "applications") — a different bug, not the phone
pattern — so the marker was restored. Only the four phone-test markers
come out. An earlier version of this section claimed the failure was
"verified on clean main via git stash"; that check was invalid (the
stash could not revert committed marker removals, so it ran on the
branch). On clean main the test xfails: 20 passed, 5 xfailed, no
failures.
```

---