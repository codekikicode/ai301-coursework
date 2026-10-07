# Procedure: how this skill grades a plan package
<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order
1. In live mode, read `scope.md` first and confirm the issue lives in the
   scoped source; note any house rules. Then read `rubric.md` and
   `references/evidence-guide.md`. List the rubric's checks and its verdict
   rule before grading anything.
2. Read the whole package before grading: the issue context first, then the
   repro evidence, then the candidate plan, then the candidate plan comment.
   In live mode read the issue thread and the posted repro comment first,
   then the draft plan.md and comment.md.

## Evidence gathering
3. For each check, gather exactly the evidence the rubric names, using the
   evidence guide's map of where each family lives. Quote the specific lines
   that decide the grade. In eval mode, use only the bundle text — it is the
   whole world; do not fetch anything.

## Check execution
4. Grade each check pass, fail, or ?. `?` means the evidence the rubric names
   is genuinely absent from the package — not that you did not look. Every
   grade carries a one-line quote or fact as evidence. Grade the proof, not
   the polish: a terse complete plan can pass and a long confident one can
   fail.

## Verdict assembly
5. Apply the rubric's verdict rule to the grades: accept (ready) only if
   every required check passes; on a required check, `?` counts as fail and
   yields reject (hold). There is no third verdict.
6. In live mode, hold the draft plan comment against `voice-guide.md` and
   note any broken rule in the summary, quoting the rule.
7. Output the fenced JSON block last: item, one entry per check
   (name, grade, evidence), verdict. The eval harness parses the last fenced
   JSON block, so it must be valid and nothing may follow it.