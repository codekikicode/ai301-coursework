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

---

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
