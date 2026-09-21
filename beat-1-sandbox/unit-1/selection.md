# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

**Verdict output**

## Ranked read-out

**1. #53 — PII scrubber fails to redact parenthesized US phone numbers — accept**
All 8 required checks pass. Best fit: pure Python regex fix in one file (`safety/pii_scrubber.py`), and the body hands over a runnable repro with observed output plus four named failing tests — exactly the "get better at Python" target with the least surface area. Both preferred checks pass, and it's the only one of the three with a zero-noise thread.

**2. #56 — Structural chunker silently drops documents with no headings — accept**
All 8 required checks pass. Same Python + runnable-repro + named-failing-test shape as #53; ranked below it only because the body leaves the fix direction slightly open ("as a single block or falling back to another strategy"). That is not an open debate — no thread exists and a collaborator filed it — so Scope still passes. Both preferred checks pass.

**3. #68 — Keyword search raises `ZeroDivisionError` when the index is empty — accept**
All 8 required checks pass. Ranked last of the three: no runnable repro in the body, it assumes familiarity with the xfail/manifest convention (mild insider knowledge, so *Newcomer-friendly wording* is the one preferred check that fails), and classmate `yulijasso` posted a detailed claim plus a reproduction on 2026-09-20. Per the Path Review house rule that claim is ignored and does not block — but with three accepted candidates, it's a reason to prefer the other two.

Noting one tension for the rubric rather than the run: the *Unclaimed: no fresh claim* check passes on #68 by the house rule even though the thread shows someone actively mid-work with a written plan. That's the rule working as intended here (course credit attaches to the PR), but it means the check can't distinguish #68 from a genuinely untouched issue — the ranking does that work instead.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "Community alive: maintainers respond", "grade": "pass", "evidence": "Collaborator Aburke225 authored all last 5 main commits, most recent 2026-09-16 (5 days before capture)."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16, within 3 months of capture date."},
      {"name": "Allowed to contribute: policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/assistant/generated-code mention; PR template requires only CI, tests, xfail removal — silence passes."},
      {"name": "Scope: one bounded change", "grade": "pass", "evidence": "Single regex gap in safety/pii_scrubber.py plus its tests; not an umbrella issue, no debate, labeled 'good first issue'."},
      {"name": "Scope: spec included", "grade": "pass", "evidence": "Body gives runnable repro with observed output and names 4 failing tests in tests/unit/test_pii_scrubber.py."},
      {"name": "Unclaimed: no assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Unclaimed: no open PR", "grade": "pass", "evidence": "Only PR in repo is #74 (open, for #60); the 2026-09-21 'referenced' event is a fork commit by Evin009, not a PR."},
      {"name": "Unclaimed: no fresh claim", "grade": "pass", "evidence": "comments_count: 0 — no claim comments of any kind."},
      {"name": "Newcomer-friendly wording", "grade": "pass", "evidence": "Clear title, self-contained repro, exact file and test names; no insider knowledge needed."},
      {"name": "Maintained recently", "grade": "pass", "evidence": "Collaborator commit 2026-09-16, within 3 months of capture date."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56",
    "checks": [
      {"name": "Community alive: maintainers respond", "grade": "pass", "evidence": "Collaborator Aburke225 authored all last 5 main commits, most recent 2026-09-16."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16, within 3 months of capture date."},
      {"name": "Allowed to contribute: policy", "grade": "pass", "evidence": "No AI-contribution restriction anywhere in docs/CONTRIBUTING.md or the PR template — silence passes."},
      {"name": "Scope: one bounded change", "grade": "pass", "evidence": "One behavior in ingestion/chunking/structural_chunker.py; filed by a COLLABORATOR, labeled 'good first issue', no thread debating the design."},
      {"name": "Scope: spec included", "grade": "pass", "evidence": "Runnable repro with observed output ('observed: 0') and named failing test test_document_with_no_headings."},
      {"name": "Unclaimed: no assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Unclaimed: no open PR", "grade": "pass", "evidence": "No cross-reference or connected event on the timeline; repo's only PR (#74) targets #60."},
      {"name": "Unclaimed: no fresh claim", "grade": "pass", "evidence": "comments_count: 0 — no claim comments of any kind."},
      {"name": "Newcomer-friendly wording", "grade": "pass", "evidence": "Clear title and self-contained repro, though it names two possible fix directions without picking one."},
      {"name": "Maintained recently", "grade": "pass", "evidence": "Collaborator commit 2026-09-16, within 3 months of capture date."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Community alive: maintainers respond", "grade": "pass", "evidence": "Collaborator Aburke225 authored all last 5 main commits, most recent 2026-09-16."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16, within 3 months of capture date."},
      {"name": "Allowed to contribute: policy", "grade": "pass", "evidence": "No AI-contribution restriction in docs/CONTRIBUTING.md or the PR template — silence passes."},
      {"name": "Scope: one bounded change", "grade": "pass", "evidence": "Guard an empty corpus in rag/retriever/keyword_search.py and drop the xfail marker; two named files, estimated 2-4 hours."},
      {"name": "Scope: spec included", "grade": "pass", "evidence": "States expected behavior ('index() shouldn't raise on an empty corpus') and names the covering test plus manifest id H-01."},
      {"name": "Unclaimed: no assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Unclaimed: no open PR", "grade": "pass", "evidence": "Both timeline 'referenced' events are fork commits by yulijasso; repo's only PR (#74) targets #60, not #68."},
      {"name": "Unclaimed: no fresh claim", "grade": "pass", "evidence": "yulijasso (author_association NONE, a classmate) wrote 'I'd like to take this bug' on 2026-09-20; Path Review house rule says classmates' claims must be ignored."},
      {"name": "Newcomer-friendly wording", "grade": "fail", "evidence": "No runnable repro in the body, and it assumes knowledge of the xfail/manifest-id convention ('manifest id H-01')."},
      {"name": "Maintained recently", "grade": "pass", "evidence": "Collaborator commit 2026-09-16, within 3 months of capture date."}
    ],
    "verdict": "accept"
  }
]
```
**The verdict must record `accept` for this issue.**

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Run 1 (rubric v1, full 20): 15/20, category floor met (clear-accept 4/8). Rubric was too strict on terse/good-first-issue-labeled issues and on small-but-active repos.

Run 2 (--only issue-01,issue-04,issue-06,issue-19,issue-20, rubric v3): 4/5 - 01, 04, 06, 20 flipped; 19 still failed both scope checks.

Run 3 (--only issue-19, rubric v3.1): 1/1, issue-19 accept.

Run 4 (full 20, rubric v3.1): 20/20 PASS, all five categories 100% - this is the run recorded in eval-run.txt.

Note about setup: On Windows, the native claude.exe ignored piped stdin ("no stdin data received in 3s"), so I made a one-line local change to run_eval.py passing the prompt as an argument, and set encoding="utf-8" on subprocess output to stop cp1252 decode crashes. No grading logic, model, or scoring lines were modified.


**Issue analysis**

issue-20 (source: excalidraw/excalidraw#11811). Gold label: reject. My rubric's current decision: reject (rubric v1 had accepted it).
Why v1 accepted: every check passed - huge active repo, no assignee, no linked PR, no claim comments, silent contribution policy, and a polished, detailed writeup. 

What v1's scope check could not see: the ask is a new feature spanning the toolbar, element system, export pipeline, and app wiring, with the key asset "Logo asset TBD" - a multi-subsystem feature with undecided parts, not a bounded first issue. I added that pattern to the fail list of "Scope: one bounded change" and re-graded with --only: the skill now rejects it, matching the gold label.

**Check rationale**

Quoted check: 
*"Scope: one bounded change" - "One coherent piece of work (code, docs, or tests) a newcomer could plausibly land in one PR. Fails only if: umbrella/tracking issue; design still openly debated; a maintainer flags core internals or states the work is unsuitable for newcomers; usage/support question; or a new feature spanning several subsystems with key parts undecided (e.g. "asset TBD"). Docs-only tasks, small bugs with identified causes, and terse good-first-issue-labeled asks pass even when multi-file. A bug report with a clear symptom and candidate causes is bounded work even if the fix likely touches performance-sensitive code"*

Reasoning: 
v1 failed four clear-accept issues with this check by reading polish as scope (a one-sentence good-first-issue bug, a multi-page docs task) and by inferring "core internals" itself on a symptom-and-causes bug report. The evidence guide says to grade the size of the work, not the writeup, and only a maintainer's word should sink an internals-touching issue, so both corrections are baked into the wording.

---

**Trade-offs**

What the quoted check gives up: the "clear symptom and candidate causes" clause can green-light a genuinely hard performance bug a newcomer can't finish, and "several subsystems" is a judgment call that could sink a suprisingly well-scoped feature. 

Canary in the coal mine moment: After updating my rubric for the final time, I re-ran issue-20 (--only) and it still rejects (good - no over-correction), and issue-19 accepts; the final full run stayed 20/20, which is how the aforementioned adjustment flipped no currently-correct verdict.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**


1. Fit to interests and time: #53 is a pure-Python regex fix in one file plus its unit tests - exactly the "get better at Python" target in my fit profile, with the least surface area of the three accepted candidates. The body includes a runnable repro with observed output and names four failing tests, so reproduction in Unit 2 should fit comfortably in the time window.

2. What the verdict identified correctly: it caught the zero-noise thread (#53 is the only one of the three with no claim or fork activity), the runnable repro, and the policy silence. What I weighed that the rubric could not: #68 shows a classmate mid-work with a written plan - the house rule says that doesn't block, but I'd rather not collide with a classmate's plan on my first contribution. #56 leaves the fix direction open ("block or fall back"), which means more design latitude than I want for a first issue. The rubric also can't judge my own familiarity: phone-number regex is comfortable ground given my Java/Python background.

3. Anticipated difficulty in claiming: unassigned, no linked PR, zero comments. Two watch-items: a fork exists whose owner "referenced" the issue in a commit (someone is lurking), and the repo is shared classroom space, so a classmate could claim it first. Path Review house rule states that a shared claim cost nothing, and claiming promptly in Unit 2 minimizes the risk.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
