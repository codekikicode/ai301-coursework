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

codekikicode

---

## Posted upstream

**Claim comment**

[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5904885781]

**Reproduction comment**

I'd like to work on #53. Per the report, the `scrub()` pattern catches dashed numbers like `555-123-4567` but lets the parenthesized
`(555) 123-4567` format through unredacted, and `detect()` reports no PII for it.

My plan: reproduce this in a clean Python environment by running the snippet from the issue body exactly as written, then running the four related failing
tests (`test_us_phone_number_redaction`, `test_us_phone_formats`,
`test_detect_phone_pii`, `test_phone_at_start_of_text`) from
`tests/unit/test_pii_scrubber.py`. I'll post my environment, the exact steps, and the observed output here -- investigation only for now, no fix promised.

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

---

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke (--limit 3): 1/3. pkg-01, pkg-03 disagreed — claim-naming
   demanded a literal number/URL; conventions only saw disclosure
   policies.
2. Canary (--only pkg-01,pkg-03,pkg-19,pkg-20): 4/4 after loosening
   claim naming, clarifying original-issue, broadening conventions.
3. Full run: 17/20, category floor unmet — pkg-03 (Steps), pkg-10
   (Original issue stated), pkg-20 (conventions).
4. Canary (--only pkg-01,pkg-03,pkg-10,pkg-20): 3/4 — pkg-03 and
   pkg-10 fixed by sharper wording; pkg-20 accepted again.
5. Read pkg-20's artifact: comments contain no disclosure at all;
   hypothesis — LLM judges under-weight absence next to a polished
   report, and the AI-saturated grading context invites treating
   disclosure as ambient. Fix: mechanical procedure (quote policy,
   search comments, fail on absence, comments' text only).
6. Canary (--only pkg-01,pkg-20): 2/2 — pkg-20 rejected.
7. Confirming full run: 20/20, every category matched, PASS.
(Pre-grading: two harness errors on Windows — the claude stdin pipe
and a cp1252 encode crash on '→' — fixed with PYTHONUTF8=1.)

**Package analysis**

pkg-20 (ghostty#13604, disclosure). Gold: reject — the repro is
excellent, but ghostty's policy requires disclosing all AI usage and
neither comment discloses. My rubric's verdicts across five runs:
reject, accept, accept, reject, reject. Why it read it that way: the
conventions check is the only required check this package can fail,
and LLM judges are unreliable at absence detection — "no disclosure
statement exists" is a null result that loses to a polished,
human-voiced report, especially inside an AI-assisted grading context
that makes disclosure feel ambient. Prose sharpenings (broader policy
forms, precedence ordering) didn't hold; what held was making the
check mechanical — quote the policy line, string-search both comments
for assistance statements, fail on absence, count only the comments'
own text as disclosure. Trade accepted: the check is narrower in
spirit than "did the author honestly convey AI use," but it executes
identically for every grader — which is what a floor category needs.

**Check rationale**

Environment recorded — Evidence: The repro report's environment record
(OS, tool/runtime versions, install or setup commands). 

Pass condition:
A stranger could recreate the environment from what is recorded; versions
match the issue's target, or the difference is called out.

It reads this way because I rejected the structural variants first: "an environment section exists" and "at least three versions are listed" are shape checks, and the calibration activity showed shape checks make
graders disagree with themselves. 

The outcome question: Could a stranger recreate it?: is one another person can apply and reach the same answer. The "difference is called out" clause came from my own package: my Python 3.14.5 against the repo's 3.11 minimum was exactly the case the check should pass honestly rather than demand version equality.

**Trade-offs**

My "Repo conventions" check reads CONTRIBUTING.md, README, and the PR template. A repo that states its contribution policy somewhere else, i.e., an issue template, a wiki page, an external doc, etc. — would let a non-disclosing comment pass, and I accept that miss. Reading only stated, findable artifacts is what keeps the check executable by a stranger: a check that
hunts "anywhere a policy might live" produces unresolvable unclear grades and quietly breaks the unclear-equals-fail rule. The eval set's disclosure wall package is caught precisely because its policy is stated
where the check looks; the trade is coverage for executability.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
