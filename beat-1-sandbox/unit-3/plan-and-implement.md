# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**codekikicode**

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

**Plan comment**

`https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-6029759436` 

Reproduced: The dashed form redacts while (555) 123-4567 passes
through unredacted (repro comment).

Diagnosis: The phone pattern's first separator class has no space, and
its leading word boundary can never start the match at the opening
paren, so the parenthesized form falls through both scrub() and
detect().

Plan: One bounded change to the phone_us pattern in
safety/pii_scrubber.py (start the match at the parentheses; allow the
space, widening separators further only if the four phone tests demand
it), plus removing those tests' xfail(strict=True) markers per
CONTRIBUTING.md. I'll verify by re-running the repro snippet and the
four phone tests.



---

## Your branch

**Branch**

`fix/53-parenthesized-phone`

**Evidence**

Before:
````
PS C:\Users\kiyal\pathreview-ai301-fa26-s1> .\.venv\Scripts\Activate.ps1
>> git checkout -b fix/53-parenthesized-phone
>> python repro.py 
Switched to a new branch 'fix/53-parenthesized-phone'
Call me at (555) 123-4567 or [REDACTED]
2026-10-07 00:57:44 [info     ] pii_detected                   count=0 types=0
[]
````

After:

````
PS C:\Users\kiyal\pathreview-ai301-fa26-s1> .\.venv\Scripts\Activate.ps1        # prompt should regain (.venv)
(.venv) PS C:\Users\kiyal\pathreview-ai301-fa26-s1> git stash
Saved working directory and index state WIP on fix/53-parenthesized-phone: f89c06f chore: track five more manifest entries against the tracker
(.venv) PS C:\Users\kiyal\pathreview-ai301-fa26-s1> pytest tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_mixed_pii_and_text
======================= test session starts ========================
platform win32 -- Python 3.14.5, pytest-9.1.1, pluggy-1.6.0
rootdir: C:\Users\kiyal\pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: anyio-4.15.1, asyncio-1.4.0
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 1 item                                                    

tests\unit\test_pii_scrubber.py x                             [100%]

======================== 1 xfailed in 0.42s ========================
````
## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1 : cp1252 encoding crash (Windows, 0 graded); 

Run 2 : 18/19 + pkg-02 ERROR; partial re-grade --only pkg-02 → accept; patched executability + honest-uncertainty rows, 

Canary run: --only pkg-14,pkg-10,pkg-17,pkg-18 → 4/4; 

--save-run 20/20, pkg-14 analysis, check rationale, trade-offs.

**Package analysis**

```
- (pkg-14, clear-accept): gold accept, my final verdict accept. Its plan named files/areas but deferred exact functions to "after tracing with debug logs, which I have working," and stated a mechanism not yet traced; my original wording failed it on executability and honest-uncertainty. 

- The patch accepts named areas + a working tracing method, and treats a grounded working hypothesis with a verification step as honesty. Both canary unbuildable packages stayed reject, confirming the loosening only reached pkg-14.
```

**Check rationale**

```
| Executability | The plan's change description: files or areas named, approach, order of work | Passes if the plan names the files or areas to change and work can start without asking the author anything; a named tracing/debug method with a working setup counts for details the plan defers with a stated reason. Fails only if no files or areas are named, or the next step needs information only the author has | required |
```

Reasoning:

```
A strict "stranger could start editing" reading failed a plan that deliberately defers function names behind a working debug method; fail was narrowed to "no files or areas named, or next step needs author-only info
```
**Trade-offs**

The loosened executability can pass plans that pin exact edit points only at build time (precision arrives late); the honest-uncertainty check can no longer fail a plan merely for asserting an unverified mechanism — it needs the evidence contradiction + no verification path.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
S