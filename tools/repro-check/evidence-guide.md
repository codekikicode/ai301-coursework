# Evidence guide: where proof lives in a reproduction package

I'm Kiyali, a student contributor working through CodePath's AI301 course. When I comment on an issue, I am investigating a reproduction: readers can expect me to name what I ran, show what I saw, and deliver work what I have actually done. I am a guest in the maintainer's repo: specific, honest, and never louder than my evidence and/or skill level.

## Environment

**Feeds rubric check: Environment recorded**

- Where it lives: in an eval bundle, the repro report's environment/setup section, read against the repo-facts block's stated versions where given. In Live mode, the environment block in the draft repro report, plus the issue body where the reporter names their own setup.

**What good looks like:** 

-OS, tool/runtime versions, and install or setup commands are named so a stranger could recreate the environment; where the report's versions differ from the issue's stated target, the difference is called out in the text rather than left implicit.

## Steps

**Feeds rubric check: Steps followable**

- Where it lives: the numbered steps of the repro report, from starting state through trigger. In Live mode, the steps section of the draft.

**What good looks like:** 

- Every step is an action a stranger can execute verbatim (a command or an unambiguous instruction); following them in the recorded environment reaches the failing behavior; nothing required is left implied ("configure as usual") or referenced to files outside the report.

## Behavior shown

**Feeds rubric checks: Original issue stated Behavior matches issue**

- Where it lives: the report's restatement of the issue and the output excerpts, logs, and screenshots quoted below it, read line by line
against the issue body's description of expected vs. actual behavior. In live mode, the corresponding sections of the draft, read against the Live issue.

**What good looks like:** 

- The restatement tracks the issue's own words: expected vs. actual — closely enough that a reader knows which reported behavior is being tested; the quoted artifact then shows that behavior (same message, same symptom), or, for an honest cannot-reproduce, the closest corresponding output with the difference from the issue's description stated plainly.

## Honesty

**Feeds rubric check: Honest outcome**

- Where it lives: the report's outcome/conclusion sentence, read against its own quoted artifacts immediately above it. In Live mode,
the draft's conclusion against its own pasted outputs.

**What good looks like:** 

- The conclusion claims nothing the artifacts do not show. "Cannot reproduce" passes when the steps were run exactly as written and the closest observed behavior is shown; "reproduced"
fails when the artifact shows an adjacent behavior, no matter how confidently it is stated.

## Comms

**Feeds rubric checks: Claim names its issue, Repo conventions**

- Where it lives: the claim comment's opening lines (read against the issue title/body), and both comments' text read against the repo-facts "contribution policy" line plus any issue/PR templates the repo states. In Live mode, the drafts against the live issue thread and the repo's CONTRIBUTING/docs.

**What good looks like:** 

- The comments follow the repo's stated conventions.
  Work mechanically, in order: (1) quote the repo-facts "contribution
  policy" line back to yourself;   (2) if that line requires disclosing AI assistance, search both
  comments for any AI-assistance statement: names of AI tools,"AI-assisted", "generated with", "with the help of" -- and if neither comment contains one, the check FAILS, even if both comments read human-written; a human-sounding voice is not disclosure. Only statements inside the two comments' own text count as disclosure; anything outside them, including how the package or its grading context was produced -- does not.

---