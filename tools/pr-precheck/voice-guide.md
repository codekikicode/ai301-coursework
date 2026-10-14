# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2 and carried it through week 3; paste your filled voice-guide.md
here, whole. It is not re-authored and it is not graded as new work
this week.

Then reread it with the PR in mind. Your comments promised, reported,
and committed to an approach; a PR title and description ask a
maintainer to spend review time on your work. If your rules do not
cover that register (for example: how a title earns its thirty
seconds, how a description promises exactly what the diff contains,
how a disclosed shortfall is worded so it reads as honesty rather
than apology), extend the guide with what it needs. Extending is
allowed and encouraged; starting over is not required.

Live mode reads this file and holds your draft PR title and
description against it, reporting any rule your draft breaks. Eval
mode ignores it entirely, because your voice is yours and carries no
gold labels.
-->

# Voice guide: how I talk upstream

## Who I am in threads

I am Kiyali Ross, a student contributor and Information Systems senior
from Brooklyn College. I am currently working through the AI301
course.

## Rules I write by

**Rule 1: Promise investigation, never fixes or dates**

Wrong: "I'll have a PR up by Friday."
Right: "I'm going to try to reproduce this and will post what I find."

**Rule 2: My proof in my own words**

Wrong: "Same as above, can confirm."
Right: Developer's own environment, steps, and output quoted.

**Rule 3: Disclose AI assistance when the repo documentation asks**

README.md should explicitly state that the developer is expected to
disclose any and all AI assistance.

**Rule 4: Claim only what the artifacts show**

Wrong: "Reproduced." (when the log shows something adjacent)
Right: "I could not reproduce; here's what I observed instead."

**Rule 5: The title earns its thirty seconds**

A maintainer skims the title to decide whether to spend review time.
It says what changed and where, not that a change happened.

Wrong: "Fix bug" / "Update themes.gitconfig"
Right: "Remove duplicate file-decoration-style from gruvmax-fang theme"

**Rule 6: The description promises exactly what the diff contains**

Every template section is filled truthfully, and I tick only the
testing boxes my evidence shows. The description is a contract with
the reviewer: nothing claimed that a hunk or an output line doesn't
back.

Wrong: ticking "unit tests pass" when lint failed
Right: pasting the failing check's output with the reason it failed

**Rule 7: A disclosed shortfall reads as honesty, not apology**

When something is left out or could not run, I say so plainly, with
the reason — one sentence, no hedging. Honesty keeps the faithfulness;
apology-padding makes reviewers trust the rest less.

Wrong: "Sorry I couldn't get the integration tests working, hopefully
this is fine!!"
Right: "make test-integration reports no tests ran; the repo's docs
say that's expected, so the output is pasted as-is."

## Things I never post

- Deadline promises
- +1/piggyback comments
- Reproduction claims without pasted artifacts
- Claims of coverage the evidence doesn't show ("all tests pass" with
  no pasted output is the classic)
- Apology-padding around an honest, disclosed shortfall