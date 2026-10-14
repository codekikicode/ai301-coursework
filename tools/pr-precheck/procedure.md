# Procedure: how this tool grades a PR package

## Read order

1. Live mode only: read `scope.md` first. If the `Repo:` line still
   carries its placeholder, stop and tell the student to fill it. If the
   PR targets a repo the scope does not name, refuse to grade. Note the
   house rules for the summary. (Eval mode skips this step entirely;
   the bundle is the whole world.)
2. Read `rubric.md` and `references/evidence-guide.md`. List the
   checks, their weights, and the verdict rule before grading anything.
3. Read the package in this order: the repo facts → the issue and its
   thread highlights → the plan context → the candidate PR (title,
   description, commits, then the diff) → the test evidence. The plan
   comes before the diff on purpose: you cannot spot a diff doing more
   or less than the plan if you met the diff first. While reading, note
   down: the plan's named files, scope boundary, steps, and test plan;
   every ask the repo facts state; the diff's file list and the purpose
   of each hunk; each claim the title and description make; every
   command and outcome in the test evidence.

## Evidence gathering

4. Gather the pairings the rubric's checks name, using the evidence
   guide's map of where each family lives (eval bundle vs. live files):
   - Plan fidelity: the plan's named files against the diff's file list
     (`git diff main...HEAD --stat` live); then each hunk against the
     plan's steps and deviation notes. Quote any file or hunk the plan
     does not name.
   - Description accuracy: list each claim in the title and description; check each against the diff's hunks; quote any contradiction.
   - Test evidence: for each item in the plan's test plan and each check the repo states, find the matching run and its observable outcome in the evidence, or a specific claim of the outcome (named command + result), or the honest note explaining its absence. Quote the output line or the note.
   - Diff quality: scan every hunk for debris and off-topic edits; quote the offending lines.
   - Standards: list each ask the repo facts state; find where the title or description answers it, and quote both sides.
5. Record one quotable line per check as you gather it. Do not re-read the whole package once a check's evidence line is in hand.

## Check execution

6. Grade the checks in rubric order, each pass, fail, or unclear, each
   with the one-line fact or quote that decided it. If the evidence a
   check names is genuinely absent — you looked, using the evidence
   guide's map — grade unclear; never infer missing evidence. Grade the
   proof, not the polish: a terse complete PR can pass and a long
   confident one can fail. A check may be graded from its gathered
   evidence without re-reading the package.

## Verdict assembly

7. Apply the rubric's verdict rule to the grades: accept only if every
   required check passes; unclear on a required check counts as fail
   and yields reject. Preferred checks never change the verdict.
8. The check whose evidence goes in the summary as the deciding line is
   the first failing required check in rubric order. When nothing
   failed, say what nearly decided it instead: the weakest passing
   line.
9. Live mode only: hold the draft title and description against
   `voice-guide.md`; list any broken rule in the summary, quoting the
   rule and the draft line. This never changes the verdict.
10. Output the readable per-check summary first, then the fenced JSON
    block last: item, one entry per check (name, grade, evidence),
    verdict. It must be valid JSON and nothing may follow it.