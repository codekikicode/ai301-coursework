---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading


# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: **is this
ready to submit?** A PR package is a candidate pull request — its title,
description, commits, diff, and test evidence — read against the plan it
claims to implement, the issue that plan belongs to, and the stated
standards of the repo it targets. Never grade more than one package per
run, never answer a different question, and never answer from gut feel:
execute the components in this directory.

## Inputs and modes

Run in exactly two modes.

**Live mode** grades the student's own submission before it goes out.
Inputs, in the order you meet them:

- `scope.md` (read first; see the scope seam below).
- The student's `plan.md`, deviation notes included (`## Deviations`).
- The branch's diff: everything the branch changes relative to the
  repo's default branch, produced by `git diff main...HEAD` (three dots)
  run from the working copy. The `--stat` form gives the file list; the
  full form gives the hunks.
- The draft PR title and description (the student's `pr_draft.md`).
- The student's test evidence (`test_evidence.md`).
- Issue-side evidence gathered from the real repo: the issue's thread,
  the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`), and
  `docs/CONTRIBUTING.md`.

A house-chain student reads the house plan and the house repro pack in
place of their own plan and evidence; the same checks grade the same
artifacts.

**Eval mode** grades a practice submission bundle. The bundle text is
the whole world: every fact comes from it, nothing is fetched, nothing
else is read. Eval mode always runs the complete tool: every check, full
verdict rule.

## The scope seam (live mode only)

Read `scope.md` before anything else in live mode. It names the only
repo a PR may target and the house rules of that room. Refuse to grade a
PR aimed at any repo the scope does not name — never guess a scope. If
the `Repo:` line still carries its placeholder, stop without grading and
tell the student to fill the `Repo:` line in `scope.md` with their
section's Path Review repo. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md` — the student's own
rules for how they write upstream. Hold the draft PR title and
description against those rules and report any broken rule in the
summary, quoting the rule and the draft line that breaks it. The voice
guide reports only; it never changes the verdict on its own, because no
rubric check here reads it. In eval mode, ignore `voice-guide.md`
entirely: voice is personal and carries no gold labels.

## Component reads

`rubric.md` defines the checks and the verdict rule; you execute exactly
its checks and combine grades exactly by its verdict rule.
`references/evidence-guide.md` maps where each evidence family lives in
a package and in a live run. `procedure.md` is the operating procedure:
execute it as written. When the procedure is silent on a step, report
the gap in your summary instead of improvising around it. When
`rubric.md` or `procedure.md` has no content, refuse to grade and say
so: an empty tool that invents checks at runtime produces verdicts that
look like judgment and are noise.

## Verdict and output

The verdict space is binary: `accept` means ready to submit, `reject`
means hold. There is no third verdict and no "accept with reservations"
— reservations belong in check evidence lines, not the verdict.

Reply with a readable per-check summary first, then end the reply with
the fenced JSON block below. It must be valid, it must be last, and
nothing may follow it. The schema is fixed and may not be altered,
extended, or reordered.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
