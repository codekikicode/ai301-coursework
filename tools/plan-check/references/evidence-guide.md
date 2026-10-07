# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: the candidate plan's stated cause ("Cause:" line or
diagnosis section), checked against the "Repro evidence" block's
Expected/Actual in the same bundle. In live mode, the diagnosis section
of draft plan.md, checked against the repro comment posted on the issue
thread.

What good looks like: the cause names a specific mechanism (which
component, which state, what goes wrong), and that mechanism explains
the behavior the repro evidence actually shows. A cause that contradicts
the quoted evidence, or that describes a different bug than the one
reproduced, fails — even if it sounds confident.

## Scope

Where it lives: the plan's scope statement — the "In:"/"Out:" lines, or
"what I'll change / what I won't touch." In live mode, the scope section
of draft plan.md.

What good looks like: the plan names each file or area it will change
AND draws an explicit boundary — what it will not touch. A fix described
as "minimal" with no out-of-scope line is not bounded; a plan whose
boundary is missing or vague cannot pass, because nothing rules out a
drive-by rewrite.

## Executability

Where it lives: the plan's change description — files named, approach,
order of work. In live mode, the approach and file list in draft plan.md.

What good looks like: a stranger could start editing without asking the
author anything. The plan names a specific file (or function/area within
one) and a specific change to make there, in steps small enough to work
through one at a time.

## Test plan

Where it lives: the plan's "Test:" section, mapped onto the numbered
steps in the repro evidence block. In live mode, the test-plan section
of draft plan.md, mapped onto the unit 2 repro steps.

What good looks like: the plan says which repro steps (or which automated
check exercising the real code) get re-run after the fix, and what
observable output is expected at each step — "step 3 shows X without
doing Y," not "the tests pass." If the unit 2 repro was a stand-in script,
good looks like turning its inputs into a check that runs the real code.

## Honesty

Where it lives: the plan's risks and unknowns section, and in live mode
the `## Deviations` heading in plan.md (filled after the build).

What good looks like: stated unknowns ("haven't tested the force-push
path," "not sure which callback fires first") read as honest scoping, and
a mid-build deviation is recorded under Deviations with what changed and
why. Total absence of any risk on a non-trivial change is a flag, not a
strength — it usually means the plan was not pushed on. (For grading:
absence is not a fail; only overclaiming — stating as certain what the
evidence contradicts or does not cover — fails.)

## Comms

Where it lives: the candidate plan comment, read against the "Thread
highlights" section (or the live thread) and the "Repo facts" block —
the bug report template's asks, CONTRIBUTING.md's contribution policy,
and any AI-use disclosure requirement. In live mode, draft comment.md
read the same way against the posted thread.

What good looks like: the comment is thread-aware — it acknowledges the
maintainer's stated constraints (e.g., selective review bandwidth, a
template field the issue left empty) and any required disclosures, and it
states what will be done in a sentence or two. Boilerplate that ignores
the repo's stated policies, or a comment posted against the wrong repo's
conventions, fails this family.