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

[(https://github.com/codepath/pathreview-ai301-fa26-s1/pull/184)]

**Branch**

fix/53-parenthesized-phone

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

*Run history: oldest → newest (quoted from each run's own output):*

1. First full run (`eval-run-v1.txt`, written 2026-10-12T06:08:04Z):
   "categories: clear-accept 1/7  not-tested 4/4  silent-drift 4/4
   standards-wall 2/2  unreviewable 3/3" / "agreement: 14/20 scored
   items  (bar: 18/20: below the bar)". All 13 reject packages agreed;
   the six disagreements were all clear-accepts, five flagged
   "failed: test-evidence" and three of those also
   "failed: test-evidence, unsubstantiated-claims" (pkg-05, pkg-08,
   pkg-19).

2. Tuning run (`--only pkg-05,pkg-08,pkg-11,pkg-13,pkg-16,pkg-19,pkg-02,
   pkg-03,pkg-04`, after loosening the test-evidence pass condition):
   terminal reported "agreement: 9/9 scored items" — all six
   disagreements flipped to agree and the three canaries (pkg-02
   clear-accept, pkg-03 silent-drift, pkg-04 not-tested) held their
   previous verdicts. Partial runs refuse --save-run, so this run
   exists only as console output, not a file.

3. Confirming full run (`eval-run.txt`, written 2026-10-12T06:45:50Z —
   the submitted run): "categories: clear-accept 7/7  not-tested 4/4
   silent-drift 4/4  standards-wall 2/2  unreviewable 3/3" /
   "agreement: 20/20 scored items  (bar: 18/20: PASS)".

*Environment note:* my first two harness attempts graded nothing ("20
item(s) errored; fix and re-run." / "claude exited 1: Warning: no
stdin data received in 3s...") — a Windows pipe-encoding failure
(cp1252 vs the '→' character in package text), fixed by running with
PYTHONUTF8=1. Zero packages were graded, so they carry no score.

**Package analysis**

*Package:* pkg-05 (nushell/nushell#18848 — keybinding merge drops
same-name bindings on different keys). Category: clear-accept.

*Gold label:* accept

*My rubric's verdict:** accept (agree — confirmed in eval-run.txt)

*Why the rubric decided this way:*
The load-bearing evidence is observable: the issue's repro script
re-run before and after, with the table showing one `atuin` row before
and two rows (ctrl-r and up-arrow) after — the expected-after state is
visible, exactly per the plan's test plan. The remaining proof is
stated as specific, checkable claims: "cargo test -p nu-protocol
passes (312 tests); fmt and clippy clean," and "same-key redefine
prints the one-time warning." Under my calibrated `test-evidence`
condition, a named command with a stated outcome counts as reporting,
so the check passes on the observable repro plus those claims. The
diff is one hunk in the planned file (plan-fidelity pass), the
description's claims match the hunk (description-accuracy pass), and
the repo's stated asks — reference the issue, stay small — are met
(standards-compliance pass).

One nuance: my preferred `unsubstantiated-claims` check still fails on
this package, because the suite results are claims without pasted
output behind them. That's deliberate design — a preferred check
reports without holding — and it's the same judgment my PR's
description relies on when it states check results concisely.

**Check rationale**

*Check:* `test-evidence` (required)

*Evidence (as stated in my rubric.md):*
The test evidence block, read against the plan's test plan and the repo's stated checks — eval: "Test evidence" against "Plan context"'s test plan and any checks named in "Repo facts"; live: `test_evidence.md` against the PR template's Testing section and the repo's own checks.

*Pass Condition (as stated in my rubric.md):*
Passes if the plan's own test plan is visibly executed against the branch: at least one observable outcome tied to the issue's behavior appears (the repro or its equivalent run, with output showing the expected-after state), and every remaining test-plan item or repo-stated check is covered by a shown result, a specific checkable claim (a named command and its outcome, e.g. "cargo test -p ignore passes (214 tests)"), or an honest "could not run, here is why" note. Fails only if there is no evidence at all; if no observable outcome for the plan's test plan appears anywhere; if the output shown does not demonstrate the expected-after state or shows it failing while claiming success; or if the evidence is unrelated to the issue and plan. Checks the author cannot run before the PR opens (CI gates) are never required; an unticked box or honest note covers them. A failing check reported honestly with its output passes.

*Why it reads this way:*
My first version required observable output for every test-plan item *and* every repo-stated check, and failed "a claimed result with no output behind it." My first full run agreed on all 13 rejects but false-rejected 6 of 7 clear-accepts (14/20). Reading pkg-05 and pkg-11 showed what the gold standard accepts: the observable repro before/after is the load-bearing evidence, while suite results may be stated as specific checkable claims ("cargo test -p ignore passes (214
tests)") — a claim with a named command and outcome is reporting, not proof-of-nothing. CI-gated checks can't run before a PR opens, so
they're never required; an unticked box or honest note covers them.

After loosening the row, I re-graded with canaries from every category the change could touch (pkg-02 clear-accept, pkg-03 silent-drift,
pkg-04 not-tested): 9/9, no flips. The confirming full run went 20/20 with every category floored.

**Trade-offs**

- *Checkable claims vs. pasted output:*
  My `test-evidence` check accepts a suite result stated as a specific claim ("cargo test -p nu-protocol passes (312 tests)") rather than requiring pasted output    for every check.
  What was gained: agreement with the gold standard on the clear-accept category (six packages flipped, 14/20 → 20/20), because real PRs summarize suite results.    What was given up: the check can't catch a confident, specific-sounding false claim on its own — that hole is deliberate, which is why `unsubstantiated-claims`    exists as a *preferred* check (reports, never holds) and why the not-tested packages still fail (they have no observable outcome at all).

- *Honest disclosure vs. automatic hold:*
  The rubric passes disclosed shortfalls — an unticked CI box, "no tests ran" integration, a
  retained xfail marker — instead of equating "less than everything" with "hold."
  What was gained: the verdict matches how maintainers actually
  read PRs, and clear-accept packages with honest gaps don't get false-rejected.
  What was given up: the tool can print "ready to submit" for a PR with a known red check if the description discloses it — it deliberately delegates that
  judgment to the developer reading the evidence. The live run showed both sides: the same disclosure rule that would have permitted my honestly-documented
  failing check also caught me when the story was wrong — the tool rejected twice (a real fifth-marker defect, a false "verified on clean main" claim) and only
  accepted once the artifact matched the description.
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
