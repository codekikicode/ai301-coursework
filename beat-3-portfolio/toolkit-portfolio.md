# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Kiyali Ross

## Featured Tools

## Featured Tools

Three or four tools, presented in depth. Open with a few sentences
on why you chose these.

Full credit asks the featured set to show real change: **at least two** of your featured
entries should show a tool that visibly moved through use. An honest entry for a tool that
barely changed — saying so, dating what did happen, and giving the reason — earns the solid
middle tier and never fails you.

Each tool's honest limit is not written here. It goes in the tool-limits list at the
bottom of this page, one line per featured tool, so that the limits sit together and can
be read as a set.

These four earned the feature slots because each one failed me in a way I could not have
predicted at install time, and each failure left a visible mark on the tool or on how I
use it. The issue-scout shaped what I chose to work on; voice-gate and ship-gate are the
two gates my work actually passed through before leaving my machine; plan-check is the one
that graded my thinking against the repository itself and caught me asserting things I had
not verified. In every case the tool became mine in the patching, not the installing.

**issue-scout**

**What it is, and the judgment hole I wrote:** my issue-selection tool: two `gh search issues`
queries with ranking filters drive a scan, and my rubric grades each candidate. The judgment
hole I wrote is the rubric itself — scope feasibility, claim freshness, spec quality, fit,
repo health, and an AI-policy check — every threshold in it is a decision I made about what
"claimable by a student" means.

**How it evolved, dated:** v1 was tuned to the unit-1 sandbox and rejected nearly everything
real in the wild (October 2026). On my TF's direction I moved to the AI 301 Issue Selection
site and loosened three checks — 60-day staleness windows for claims and PRs, a clearer
spec bar (v2, October 2026). When the scout flagged its own inconsistency — accepting a
stale-assignee case on OpenSearch #4253 — I patched the claim logic (v3, October 2026). In
Unit 6 I replaced my "one bounded change" scope check with the staff scope-feasible row,
because scope was rejecting issues I could have done (October 2026).

**Evidence:** final grade line from my run: `CTSM#2256 accepted 10/10` alongside
`django-rusty-templates#27 rejected` — the rejection on grounds I would have missed
unaided: an AI policy banning LLM help on good-first-issues plus a 17-day-old
owner-approved claim. The v3 patch was driven by a failure the scout reported about
itself.

**ship-gate**

**What it is, and the judgment hole I wrote:** a PreToolUse hook that runs my manifest of
repo checks plus a PR pre-check before any outgoing command. The judgment hole I wrote is
the ship-manifest: which checks count as "this branch is shippable" on this repo, on this
machine — including the decision to document a check that *fails on unmodified master*
(3425-test Perl suite, exit 254, 1052 pre-existing Windows failures) instead of hiding it.

**How it evolved, dated:** it fought me for a week before it ever fired (November 2026).
Layer 1: stale Claude sessions don't reload hooks — learned by retaught-full-exit.
Layer 2: the hook called `python3`, a broken Microsoft Store stub on my box — changed to
`python`. Layer 3: the matcher said "Bash" but my Claude Code's shell tool is literally
named "PowerShell" — and `Bash|PowerShell` alternation does not match. Layer 4, the real
root cause: both course scripts gated on `tool_name != "Bash"` — I patched them to accept
`("Bash", "PowerShell")` with sed and reported all of this in
#dts-fa26-ai301-build-support (November 2026).

**Evidence:** the verification, live — ship-gate STOPs `gh pr create` (exit 2) mid-session,
after silently passing it for days. And from my Unit 7 work: the red→green pair of the new
failtest it shipped alongside — `not ok 1189 - namelist_opts_infile_conflict` on
unmodified master vs `ok 1189` with my fix, with CSMDATA set both times.

**plan-check**

**What it is, and the judgment hole I wrote:** a skill that grades plan.md + plan-comment.md
against five checks (diagnosis-grounded, scope-bounded, executability, honest-uncertainty,
thread-and-conventions). The judgment hole I wrote is the plan itself: which code claims I
was willing to stake the plan on, and the scope lines — in-file duplicates stay
last-one-wins, `merge_nl` untouched — which are mine, taken from the issue text.

**How it evolved, dated:** reject → reject → accept across three runs (November 2026). Run
1 failed diagnosis-grounded: no posted reproduction existed yet, so I wrote and posted a
standalone repro comment to ESCOMP/CTSM#2256 (comment id …-7086475038). Run 2 failed
honest-uncertainty: I had ruled out `die_on_conflict` with a "later files override earlier"
argument that contradicts first-write-wins, and the checker verified against the live repo
that buildnml passes one combined -infile. I dropped the unverifiable claim and said so in
the plan. It also found two design risks I had missed: `start_ymd` injected into -namelist
and `finidat`/`nrevsn` injected into the infile. Run 3: accept.

**Evidence:** its verdict block, quoted from my session:
`honest-uncertainty: fail. States merge_nl is "first-write-wins" yet asserts "later files
intentionally override earlier ones"... buildnml passes a single combined -infile.` — and
the final `Verdict: accept`. The plan it accepted is the one my merged fix was built from.

**voice-guard**

**What it is, and the judgment hole I wrote:** a hook that holds outgoing words (issue
comments, PR bodies) against my voice guide before they can leave. The judgment hole I
wrote is the voice guide — no promised dates, no unverifiable claims, disclose AI use —
plus the final settings.json wiring: matcher "PowerShell", backslash paths, `python` not
`python3`.

**How it evolved, dated:** it never fired on the first wiring test (October 2026). Three
causes, three fixes: `ln -s` under MSYS made silent copies instead of symlinks (pointer-file
fallback); the machine had no Python at all, so the hook's `python3` could never have run
(installed 3.12, rewrote the hook); the checker couldn't launch npm's claude.CMD via
subprocess on Windows, so I installed the native claude.exe build — all reported in
#dts-fa26-ai301-build-support (October–November 2026). Later it needed the same
PowerShell/tool_name patch as ship-gate once I found that root cause.

**Evidence:** live verification — voice-guard STOPs `gh issue create --help`, and both my
posted comments (the claim comment and the repro comment on ESCOMP/CTSM#2256) passed
through it carrying my AI-disclosure line, which now reads as a habit rather than a
compliance step.

## Inventory

One line each for the rest of the toolkit: what it is and where it
stands (one bullet per tool; a compact sentence or two is fine).

- repro-check: my reproduction grader, with the wild-scoped rubric I wrote myself in Unit 6
  after finding the installed one was still the staff template; accepted my repro report on
  the second run, and its "quote, don't paraphrase" rule later caught me in plan.md.
- pr-precheck: the PR hygiene checker ship-gate invokes; installed with the Unit 7 toolkit,
  now runs as part of every gate check on the branch.
- pr-monitor: the Unit 8 watcher that reads PR state and drafts follow-ups per my playbook;
  installed and configured, doing its first real watch cycle on my open PR.
- gh (GitHub CLI): the hands for everything — issue search, claim, comment, repo defaults,
  and the eventual `gh pr create`; reliable all term, which is exactly what a hands tool
  should be.
- Claude Code: the runtime all the hooks live in and the executor for graded commands;
  the Windows quirks above (shell tool name, stale sessions, claude.CMD) were all lessons
  about how it actually behaves on this machine versus how the course materials assume.

## The Arc

The story of the toolkit in order: friction, change, result, dated.
Your weekly Toolkit entries are the source; read your own record and
tell it oldest first.

Write one block per beat, in the shape below, oldest first. Keep all four labels on every
beat, each on its own line. The `Result:` line is what the beat was for: it says what
happened *after* the change, which is not the same sentence as the change itself. If a beat
never reached a result, write `Result: none` — an honest beat that did not land still counts
fully as a beat.

Full credit asks for **at least two** beats whose `Result:` line names something that
actually happened afterwards. A beat about something that did not work counts fully as a
beat, and when the work happened never moves this score.

**Beat 1**
Date: October 2026
Friction: my first wild scans returned five candidates with four accepts — all from one
repo, zero diversity — and the v1 rubric rejected nearly everything real because it was
tuned to the sandbox.
Change: moved to the AI 301 Issue Selection site picks, loosened three checks on TF
advice (v2), then patched the stale-assignee inconsistency the scout flagged on itself (v3).
Result: CTSM#2256 accepted 10/10 and claimed, with a claim comment that raised my open
edge to the maintainer up front.

**Beat 2**
Date: October 2026
Friction: the voice guard never fired on its wiring test — three separate causes
(symlink-copies, missing Python, stale session) plus a subtler one (claude.CMD can't be
subprocess-launched on Windows).
Change: pointer-file fallback, installed Python 3.12 and rewrote the hook, retaught the
full exit, switched to the native claude.exe build; reported the Windows bugs in
#dts-fa26-ai301-build-support.
Result: verified live stops on outgoing commands, and every comment I posted this term
passed through it with the disclosure line intact.

**Beat 3**
Date: October 2026
Friction: the installed repro-check rubric was the staff template — nothing could be
graded until I wrote the checks; my first report failed four of five (environment not
repeatable, paraphrase dressed as a quote).
Change: wrote the wild-scoped rubric myself; rewrote the report with real terminal output,
exact quotes with verified line numbers, and inlined fixtures.
Result: accept on the second run, and a reproduction that plan-check later accepted as
grounding for my plan.

**Beat 4**
Date: November 11 2026
Friction: ship-gate never stopped a `gh pr create` test for days — silent all the way down
to the course scripts gating on `tool_name != "Bash"` while my shell is PowerShell.
Change: diagnosed in four layers (sessions, python3 stub, matcher, script gate), patched
both check scripts, rewrote settings.json, verified with canary hooks and logging.
Result: ship-gate and voice-guard both confirmed live; my ship-manifest exists with an
honest entry for a check that fails on unmodified master on this machine.

**Beat 5**
Date: November 17 2026
Friction: plan-check rejected my plan twice — first for no posted repro, then for a
self-contradiction (first-write-wins vs. "later files override"), which it proved against
the live repo and the buildnml call path.
Change: posted a standalone repro comment to ESCOMP/CTSM#2256; dropped the unverifiable
argument and said so openly; added the start_ymd/finidat/nrevsn skip design and moved the
check behind a flag so CAM's drv_flds_in path stays untouched.
Result: verdict accept on the third run — the plan that my merged fix and its test were
built directly from.

**Beat 6**
Date: November 22 2026
Friction: my new failtest "passed" on unmodified master for the wrong reason — the suite's
default inputdata root is a Yellowstone path that doesn't exist here, killing failtests
before namelist processing.
Change: set CSMDATA=/tmp/inputdata so the suite reaches the code under test; re-ran and
got the true red; then implemented the recorded-set + flagged-conflict check in
CLMBuildNamelist.pm.
Result: the manual rehearsal flipped from silent `exit: 0` to a fatal_error naming
`mksrf_lsmlon` and both sources, control runs stayed green, and the suite flipped my test
from `not ok` to `ok` with no new failures against the documented Windows baseline — the
evidence behind my opened PR.

## Limitations and What's Next

The toolkit gates words and branches well, but it still trusts my eyes for the two things
that actually bit me this term: a false-pass only I noticed (the CSMDATA default quietly
validating tests for the wrong reason) and a manifest entry that documents a broken check
rather than fixing the check. Next, I would add a manifest lint that fails when a check's
result hasn't been re-derived recently, and a "known-failure registry" that diffs suite
output against a stored baseline instead of relying on me to eyeball before/after logs.
I would also upstream the Windows hook fixes — the tool_name gate, the python3 assumption,
the Bash matcher — since every Windows student behind me will hit the same four layers.

**Tool limits.** 

- issue-ship-gate: it runs what the manifest lists; it cannot tell whether the manifest is sufficient — my false-pass scare was caught by reasoning, not by the gate, and the Windows-baseline failure is documented rather than resolved.
- issue-plan-check: it can only grade what exists on the thread and in the files — it could not see the CSMDATA environment trap, and its code-claim checking stops where the live session's access does.
- issue-voice-guard: it holds wording, not truth — a confidently wrong claim in my voice still passes; that hole is only covered because plan-check exists.
