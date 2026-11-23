# Contribution: CLM_NAMELIST_OPTS should not allow items changed to also be in user_nl_clm

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]

**Student:** Kiyali Ross

**GitHub Username:** codekikicode

**Issue:** https://github.com/ESCOMP/CTSM/issues/2256

**Pull Request:** https://github.com/ESCOMP/CTSM/pull/4344

One repository, built across Units 5 to 8 (CodePath AI 301), telling the entire story of my contribution. 

---

## Toolkit

**Unit 5: Built my issue-scout, then rebuilt its rubric twice to choose my issue**

I installed the issue-scout over my unit-1 issue-select, wrote my fit profile, and built a search strategy from two gh search issues queries with ranking filters. My scan graded five candidates with four accepts (all from one repo, srtab/daiv — zero diversity), but TF Jacob Cho directed me to pick from the AI301 Issue Selection site. There my v1 rubric rejected everything real; so I loosened three checks (60-day staleness windows for claims and PRs, clearer spec bar). When the scout then flagged its own inconsistency — a stale-assignee case on OpenSearch #4253 — I patched that too (v3). It still rejected that issue on new evidence, which told me the tool was working, not just permissive. My final picks graded: CTSM#2256 accepted 10/10, django-rusty-templates#27 rejected (AI policy bans LLM help on good-first-issues plus a fresh claim). I chose CTSM#2256.

**Unit 6:  Installed the voice guard, re-scoped repro-check and plan-check for the wild, and wrote the repo memory file**

The voice guard fought me three times before it fired: MSYS ln -s made silent copies instead of symlinks (fixed with the pointer-file fallback), my machine had no Python at all so the hook's python3 call could never have worked (installed 3.12, rewrote the hook to python + absolute path), and the first wiring test ran unblocked because my Claude session predated the settings edit. Then a subtler one: the guard's checker can't launch npm's claude.CMD on Windows (subprocess with shell=False), so I installed the native claude.exe build — reported in #dts-fa26-ai301-build-support. The memory file paid off immediately: orienting bld/ surfaced the test gap (no test sets the same variable in both -namelist and -infile), which is where my fix's test will go.

**Unit 7: Installed the ship-gate and fought Windows for a week to make it fire**

The installer wrote my ship-manifest (3 checks: validate_xml.py passes; the Perl namelist test driver fails on unmodified master on my machine — exit 254, a platform quirk I documented rather than hid; Python tests blocked, no conda). Then the hook saga: the gate silently never ran because (1) the hook called python3, which is a broken Microsoft Store stub on this box, (2) the matcher said Bash but my Claude Code's shell tool is literally named PowerShell (and Bash|PowerShell alternation doesn't match), and (3) the course scripts themselves gated on tool_name != "Bash" — I patched both scripts to accept ("Bash", "PowerShell") and reported all three bugs in #dts-fa26-ai301-build-support. Verified live: ship-gate STOPs a gh pr create.

**Unit 8: Pointed the PR-monitor at PR #4344 and let it watch**

The pr-monitor reads the PR's live state from my clone and drafts the next move
from my playbook. On its first full run (2026-11-23) it read: 1 check passing,
mergeable, REVIEW_REQUIRED, 0 comments/reviews, and a QUIET state (under a day
since the last activity by anyone but me). It drafted: "No nudge. Wait note: the
playbook's threshold is not met" — the 30-day staleness rule I wrote did its job
on day one, correctly refusing to ping a maintainer hours after the PR opened.
What fought me: the monitor refused to run until my playbook had real rules in
all four sections — twice, because my first edit never saved. What changed: the
playbook is now a written-down patience contract (14/30-day thresholds, one
nudge ever, walk-away at 60 days past it), and the monitor is how I check myself
against it weekly instead of refreshing the PR page on instinct.

---

## Why I Chose This Issue

I found this issue through the AI 301's Issue Selection site after my first wild scans went sideways. A strategy scan surfaced five candidates and accepted four — all from a single repo, srtab/daiv, which gave me zero diversity — and my v1 rubric rejected nearly everything real, because it was tuned to the unit 1 sandbox where issues arrive perfectly bounded. On my TF's advice I loosened three checks (60-day staleness windows for claims and PRs, a clearer spec bar), and later patched a stale-assignee inconsistency the scout itself flagged on OpenSearch #4253 (v3). My final picks graded: CTSM#2256 accepted 10/10, django-rusty-templates#27 rejected — its AI policy bans LLM help on good-first-issues and it had a fresh owner-approved claim.

I chose CTSM#2256 with my eyes open about its fit. My scout accepted it 10/10 but flagged the difficulty as ambitious: the change likely lives in the build-namelist layer (bld/CLMBuildNamelist.pm), Perl I haven't worked in, and the model's namelist precedence logic is new territory. Its fit read was also honest — "middling": it isn't C++ (my strong avoid), but it isn't Python either, and CTSM is a big Fortran/Perl climate model rather than a newcomer-friendly web project. What won me over is that the issue itself is a bounded, well-specified behavior change — die with a clear error when a namelist item is set in both CLM_NAMELIST_OPTS and user_nl_clm — labeled good-first-issue and bit-for-bit, with the spec written by the maintainer himself. Because the difficulty note was ambitious, I raised its open edge in my claim comment up front: I asked whether the check belongs in CLMBuildNamelist.pm and where duplicate detection fits best, and I'm waiting on maintainer direction before building. 

For Unit 6, I replaced my "Scope: one bounded change" check with the staff scope-feasible row and re-graded both picks: CTSM#2256 accepted again (one task, in-file duplicates explicitly out of scope), and django-rusty-templates#27 rejected again on the same two grounds — an AI-policy ban on LLM help for good-first-issues, and a 17-day-old owner-approved claim. 

An honest read of the scout: it fell short on its first real searches (single-repo results, over-strict scope), but every patch I made came from a failure it surfaced, it caught an AI-policy ban I would have missed, and its verdicts held steady across rubric versions. I trust it because I've watched it fail.

Claim comment: https://github.com/ESCOMP/CTSM/issues/2256#issuecomment-6869064418

**Toolkit**

- Tool: issue-scout -- my search strategy (two gh search issues queries with
  ranking filters) and my rubric, used in direct mode against the Issue
  Selection site picks.

- What it produced: a scan of five candidates with four accepts (all one
  repo), then after two rubric rebuilds, final verdicts on my site picks:
  CTSM#2256 accepted 10/10 with a "moderate" difficulty note,
  django-rusty-templates#27 rejected on AI policy plus a fresh claim.

- Difficulties: v1 rejected everything real (sandbox-tuned scope check);
  first scan returned a single-repo result set; the re-grade surfaced
  three rubric gaps: a leftover classroom house rule in the claim check,
  no rule for my own claim, and a repo-wide AI-policy check that can't
  express django-rusty-templates' label-scoped ban.

- What changed: loosened three checks on TF advice (v2), patched a
  stale-assignee inconsistency the scout itself flagged (v3), and in unit 6
  replaced my "Scope: one bounded change" check with the staff
  scope-feasible row — scope now informs (difficulty note) instead of
  rejecting.

---

## Understanding the Issue

**Problem Description**

Not a crash-bug — the maintainer says it's "technically not a bug, because it's working as it's designed." What's missing is a guardrail: the model lets you set the same namelist item in two places (CLM_NAMELIST_OPTS and user_nl_clm), silently picks one, and never notifies the user. This costs users time and energy with long debugging sessions.

**Expected Behavior**

When the same namelist item is set in both CLM_NAMELIST_OPTS and user_nl_clm, the build-namelist step should die with a clear error telling the user to change one or the other — instead of silently choosing.

**Current Behavior**

The precedence rules give CLM_NAMELIST_OPTS higher priority and silently ignore the conflicting entry in user_nl_clm. The user thinks they changed something, but they didn't. It's especially bad for B compsets, which set CLM_NAMELIST_OPTS themselves — so a user edit in user_nl_clm gets overridden by something the compset set behind their back.

**Affected Components**

The build-namelist layer: bld/CLMBuildNamelist.pm (where namelist precedence is resolved) — that's the location you flagged in your claim comment, pending maintainer confirmation. Tests would live in bld/unit_testers/build-namelist_test.pl (the Perl test driver you just ran). Also useful to note what's out of scope per the issue: duplicates within user_nl_clm itself (last-one-wins) — the maintainer explicitly carved that out as a separate, harder problem.

**Toolkit**

- Tool: Claude Code guided source tracing, plus my Unit 6 repo memory file from the   scoped orientation run over bld/.
- What it produced: the causal chain from CLM_NAMELIST_OPTS/user_nl_clm through cime_config/buildnml into CLMBuildNamelist.pm's two merge passes, and the discovery that the test suite never sets the same variable in both places (the test gap my fix's test fills).
- Difficulties: no maintainer response to my claim-comment question about where the check belongs — I proceeded on the issue text's own specification.
- What changed: nothing in the tooling; the "pending maintainer confirmation" hedge stayed in the text as an honest record.

---

## Reproduction Process

**Environment Setup**

- OS: Windows 11, MSYS2 UCRT64 bash shell
- Perl: v5.42.3 (x86_64-cygwin-thread-multi), from `perl -v`
- Repo: my fork of ESCOMP/CTSM (codekikicode/CTSM), master at
  commit 5e1da3a64f758991cf0c0b52f30cf5e3646099bf (`git rev-parse HEAD`)
- `$CTSM` below means `~/ai301-coursework/CTSM` (the clone root).
- Setup challenge 1: a plain clone is not enough. `bld/build-namelist`
  needs the cime external's `utils/perl5lib` (first error:
  'Cannot find perl module "XML/Lite.pm"'). Fixed with a targeted
  `git submodule update --init cime` (pin cime6.5.20), not a full
  git-fleximod checkout.
- Setup challenge 2: build-namelist will not run standalone without
  case XML files. Fixed by writing the two minimal fixtures the
  repo's own test harness (bld/unit_testers/build-namelist_test.pl)
  writes, into a scratch dir (/tmp/repro), passed with -envxml_dir.
  Their exact contents:

  config_cache.xml:
  ```xml
  <?xml version="1.0"?>
  <config_definition>
  <commandline></commandline>
  <entry id="phys" value="clm5_0" list="" valid_values="clm4_5,clm5_0,clm6_0">Specifies clm physics</entry>
  </config_definition>
  ```

  env_run.xml:
  ```xml
  <?xml version="1.0"?>
  <config_definition>
  <entry id="DIN_LOC_ROOT" value="/tmp/inputdata" />
  <entry id="GLC_TWO_WAY_COUPLING" value="FALSE" />
  <entry id="LND_SETS_DUST_EMIS_DRV_FLDS" value="TRUE" />
  <entry id="NEONSITE" value="" />
  <entry id="PLUMBER2SITE" value="" />
  <entry id="CLM_CMIP_ERA" value="cmip7" />
  <entry id="CLM_NDEP_FROM_CPL" value="FALSE" />
  </config_definition>
  ```
- Observed anomaly: Every run on MSYS perl prints
  "Attempt to call undefined import method ... via package
  CLMBuildNamelist", including successful runs. Cosmetic on this
  platform; ignored.

**Steps to Reproduce**

In /tmp/repro (containing the two fixtures above), with this
user_nl_clm setting one variable:

```text
&clm_inparm
 hist_mfilt = 5
/
```

1. Conflict case — the same variable set in both places. The
   -namelist flag plays the role of CLM_NAMELIST_OPTS (the docs
   inside CLMBuildNamelist.pm say so explicitly, in the precedence
   note: "1. values set on the command-line using the -namelist
   option, (i.e. CLM_NAMELIST_OPTS env_run variable)"):

   ```bash
   perl $CTSM/bld/build-namelist -envxml_dir . -csmdata /tmp/inputdata \
     -configuration clm -structure standard -glc_nec 10 -no-note \
     -res 0.9x1.25 \
     -namelist "&clm_inparm hist_mfilt=3 /" -infile user_nl_clm
   ```

2. Control case — the variable only in the file: the same command
   without -namelist.
3. Check which value won: `grep hist_mfilt lnd_in`


**Reproduction Evidence**

**Commit showing reproduction:**  None -- evidence is the terminal output below, rerun from the steps above.

Conflict case, run on master @ 5e1da3a:

```text
$ bash run_repro.sh; echo "exit: $?"; grep hist_mfilt lnd_in
Attempt to call undefined import method with arguments ("main") via package "CLMBuildNamelist"
(Perhaps you forgot to load the package?) at /c/Users/kiyal/ai301-coursework/CTSM/bld/build-namelist line 21.
exit: 0
 hist_mfilt = 3
```

Control case (no -namelist):

```text
$ perl $CTSM/bld/build-namelist -envxml_dir . -csmdata /tmp/inputdata \
    -configuration clm -structure standard -glc_nec 10 -no-note \
    -res 0.9x1.25 -infile user_nl_clm
$ grep hist_mfilt lnd_in
 hist_mfilt = 5
```

Conflict case: exit code 0, no warning or error, and lnd_in holds
`hist_mfilt = 3` — the -namelist (CLM_NAMELIST_OPTS) value won; the
user_nl_clm value was silently ignored. This is exactly the behavior
the issue reports ("it uses what's in there and ignores what the
user added to the user_nl_clm file"), reproduced on current master.

Control case: `hist_mfilt = 5` — the file is honored when nothing
conflicts, so the silent loss happens only on duplication, not from
the infile being ignored outright.

A second, independent repro (use_c13, run from bld/unit_testers) was posted to the issue thread: [https://github.com/ESCOMP/CTSM/issues/2256#issuecomment-6869064418] — or swap one to match the other.

**My findings:** 
- The issue is real today: a variable set in both CLM_NAMELIST_OPTS
  and user_nl_clm is silently accepted, CLM_NAMELIST_OPTS winning.
- The mechanism is visible in the source: at master @ 5e1da3a,
  `sub process_namelist_commandline_namelist` (line 1524) runs before
  `sub process_namelist_commandline_infile` (line 1575), and the
  merge comment at line 1541 states: "Previously specified values
  have higher precedence and are not overwritten." There is no
  duplicate detection between the two passes.
- Precedent for the fix exists in the same file: rank-0 settings
  (CLM_BLDNML_OPTS) abort with fatal_error when contradicted. The
  issue asks for that behavior one rank down.
- Test gap (from my scoped orientation run over bld/; the combined cases 
  are at build-namelist_test.pl :520 and :545–550.): build-namelist_test.pl only
  combines -namelist with --infile against empty_user_nl_clm; no
  existing test sets the same variable in both. The duplicate-check
  test belongs there.
- Commit showing reproduction: none — evidence is the terminal
  output pasted above, rerun from the steps in this report.

**Toolkit**

- Tool: repro-check (wild-scoped scope.md, my new rubric written this
  week), grading claim-draft.md and repro-draft.md as a pair.
- What it produced: first run REJECT with four fails (environment not
  repeatable, repo-relative paths, no pasted output, a paraphrase
  dressed as a quote); second run accept, all five required checks
  plus the preferred one.
- Difficulties: the installed rubric was still the staff template —
  I had to write the checks myself this week before anything could
  be graded.
- What changed: I rewrote the report to the rubric: real terminal
  output instead of "reproduced" claims, exact source quote with
  verified line numbers, fixtures inlined. The quote fix was my own
  Rule 4 catching me through a second tool.

---

## Solution Approach

**Analysis:**

`CLM_NAMELIST_OPTS` and `user_nl_clm` enter through `cime_config/buildnml` as the `-namelist` and `-infile` arguments to `bld/build-namelist`. In `CLMBuildNamelist.pm`, `process_namelist_user_input` (line 594) calls `process_namelist_commandline_namelist` (line 1524) first, then `process_namelist_commandline_infile` (line 1575), which calls `process_namelist_infile` (line 1547).

Both merge via `Build::Namelist::merge_nl` (`cime/utils/perl5lib/Build/Namelist.pm:373`), which is first-write-wins: variables already set are silently skipped. So any item set in both places keeps the `CLM_NAMELIST_OPTS` value and the user's `user_nl_clm` edit is silently discarded — exactly the behavior described in the issue. The issue asks for a clear "change one or the other" message when a setting appears in both `CLM_NAMELIST_OPTS` and `user_nl_clm`, so the check belongs in `CLMBuildNamelist.pm`.

`Build::Namelist::merge_nl` has a `die_on_conflict` option, and `process_namelist_infile` already passes `die_on_conflict =&gt; 1` for one call — but it can't be the whole fix. Its error message is generic ("A variable was already set...") and doesn't name `CLM_NAMELIST_OPTS` or `user_nl_clm`, which is exactly the clear message the issue asks for. (I initially suspected a conflict risk across multiple sequential infiles, but `cime_config/buildnml:382` passes a single combined `-infile`, so I dropped that argument rather than assert it unverified.)

Two risks to design around, both from `cime_config/buildnml` injecting content the user didn't write: (1) it always adds `start_ymd=&lt;RUN_STARTDATE&gt;` to the `-namelist` string alongside `CLM_NAMELIST_OPTS` (~line 382), so `start_ymd` must be skipped when recording `-namelist` variables; (2) for branch/hybrid runs it writes `finidat`/`nrevsn` lines into the combined infile (~line 367), so those are skipped in the comparison too. Known trade-off: a user who genuinely sets `finidat` in both `CLM_NAMELIST_OPTS` and `user_nl_clm` won't get the error — accepted, since a false blame is worse than a missed one.

The check lives in `process_namelist_infile` (where `$nl_infile_valid` already exists), behind a new option — e.g. `check_namelist_opts_conflicts =&gt; 1` — that only `process_namelist_commandline_infile` passes. The CAM `drv_flds_in` call at line 4390 doesn't pass the flag, so it's unaffected.

I reproduced this on master (`5e1da3a`): with `use_c13=.true.` passed via `-namelist` (what `CLM_NAMELIST_OPTS` maps to) and `use_c13=.false.` in the `-infile` (what `user_nl_clm` maps to), `build-namelist` completed with no error or warning, and the generated `lnd_in` contained `use_c13 = .true.` — the infile value was silently discarded. Repro details posted in this comment: https://github.com/ESCOMP/CTSM/issues/2256#issuecomment-7086475038

**Proposed Solution:**

- In `process_namelist_commandline_namelist`, record the set of variables (group + name) that the `-namelist` pass set (e.g. into `$nl_flags`), skipping known buildnml-injected variables such as `start_ymd`.
- In `process_namelist_commandline_infile` (1575 — which handles only user `-infile` arguments), pass a new `check_namelist_opts_conflicts => 1` option to `process_namelist_infile`. There, before merging each user infile, enumerate `$nl_infile_valid` with `get_group_names`/`get_variable_names`/`get_variable_value`, collect any variables present in the recorded set (skipping `finidat`/`nrevsn`), and if the list is non-empty, `$log->fatal_error` naming every duplicated variable and telling the user to remove the setting from either `CLM_NAMELIST_OPTS` or `user_nl_clm` — per the issue text.
- Out of scope, per the issue: duplicates within `user_nl` files, and no change to `merge_nl` itself (shared CIME code).

**Implementation Plan:**

- Branch `fix/2256-namelist-opts-conflict` (or per CTSM convention).
- Add the variable-set recording in `process_namelist_commandline_namelist` and the duplicate check in `process_namelist_infile` behind the new flag, passed only from `process_namelist_commandline_infile`.
- Add a test to `bld/unit_testers/build-namelist_test.pl` that passes both a `-namelist` fragment and an infile setting the same variable, and asserts the death — using the existing fixture files (`myuser_nl_clm`/`empty_user_nl_clm`) as a model. Verify it fails without the fix, passes with it.
- Run manifest checks (XML validation) and the reproduction steps; capture before/after output in `test_evidence.md`.

**Toolkit:**

- Tool: plan-check (wild-scoped), run three times against plan.md + plan-comment.md.
- What it produced: reject (no posted repro evidence) → reject (honest-uncertainty: my  plan contradicted itself — first-write-wins can't coexist with "later files override earlier ones") → accept, after it verified my code claims against the repo live and caught two real design risks I'd missed (start_ymd injected into -namelist, finidat/nrevsn into the infile).
- Difficulties: it read the actual CTSM source to check my claims — I couldn't hand-wave. It also ruled my plan-comment stays off the thread until a maintainer replies.
- What changed: posted a standalone repro comment; dropped the unverifiable multi-infile argument and said so openly; moved the check behind a flag so CAM's drv_flds_in call is unaffected; added skip-lists for buildnml-injected variables.
---

## Testing Strategy

**Repro re-run (before/after):** 
The exact steps in Reproduction Process, on my fix branch. 

- Before: exit 0, silent, -namelist value wins. 
- After (pass criteria): build-namelist dies non-zero, message names the duplicated variable(s) and says to remove the setting from CLM_NAMELIST_OPTS or user_nl_clm.

**Control re-run:** 
Variable only in user_nl_clm must still be honored (no false positive), and a conflict-free run must produce identical lnd_in to before.

- New unit test in bld/unit_testers/build-namelist_test.pl: same variable via -namelist and -infile, asserts death. Verified failing without the fix, passing with it.
- Manifest checks: python .github/workflows/validate_xml.py must pass. The full Perl suite is run as a before/after diff, since its baseline on Windows already fails (exit 254 — documented in ship-manifest.md); the criterion is "no new failures beyond baseline."

All output captured in test_evidence.md.

**Toolkit**

- Tool: ship-manifest checks plus the red/green Perl suite pair; evidence captured in test_evidence.md.
- What it produced: the new failtest red on unmodified master with CSMDATA set (`not ok`), the manual rehearsal flipping from silent `exit: 0` to the fatal_error naming `mksrf_lsmlon`, both no-conflict control runs staying green, and the post-fix suite run flipping the test to `ok` with no new failures against the documented Windows baseline.
- Difficulties: 3425 tests at roughly an hour per run on Windows; grep refused the binary-ish suite output until `-a`; the suite and any manual rehearsal share the working directory and cannot run concurrently; and the suite's default inputdata root (a Yellowstone cluster path) manufactures false-passes on any non-NCAR machine unless CSMDATA is set.
- What changed: every suite invocation now carries CSMDATA=/tmp/inputdata, and the exit-254 baseline is recorded in ship-manifest.md as a documented platform failure instead of being fought or hidden.
---

## Implementation Notes

**[2026-11-22]**

Built the fix on fix/2256-namelist-opts-conflict: the recording loop in
process_namelist_commandline_namelist (start_ymd skipped), and the conflict
check in process_namelist_infile behind check_namelist_opts_conflicts
(finidat/nrevsn skipped), enabled only from process_namelist_commandline_infile
so CAM's drv_flds_in call at line ~4390 is untouched. Wrong turns: the check
landed in three pieces across two days — a check that records but never fires
looks identical to no check until the flag is wired through; and the suite's
default inputdata path manufactured a false pass that only the manual
rehearsal exposed. PR #4344 opened the same day; ship-gate caught four
formatting defects in pr_draft.md before they went public.

**[2026-11-22]**

Plan accepted by plan-check on the third run. Key design decisions locked: check lives in process_namelist_infile behind a new check_namelist_opts_conflicts => 1 flag passed only by process_namelist_commandline_infile (keeps CAM's drv_flds_in call at line 4390 unaffected); start_ymd skipped on the -namelist side and finidat/nrevsn on the infile side because buildnml injects those itself. Wrong turn recorded: my first plan rejected die_on_conflict with a "later files override earlier ones" argument that contradicts first-write-wins — plan-check caught it against buildnml:382

**Toolkit**

- Tool: Claude Code as the implementing pair — I described each edit target, it produced the patch, I applied and verified each hunk with perl -c, grep, and rehearsal runs.
- What it produced: the three-edit patch to CLMBuildNamelist.pm, the failtest entry and fixture, and the before/after evidence pair behind PR #4344.
- Difficulties: the two-copy Edit 3 (half-applied patch, silently inert check) cost a debugging round; and the pager-mangled git diff paste made review harder than the patch deserved.
- What changed: after the half-applied edit, I started verifying each hunk with grep for its marker strings before any test run — "is the flag actually passed?" became a checklist step.
---

## Pull Request

**PR Link:** https://github.com/ESCOMP/CTSM/pull/4344

**PR Description:** 
Adapted from this story: the silent-override root cause
(CLM_NAMELIST_OPTS/-namelist merges first, merge_nl first-write-wins), the fix
(recorded -namelist variable set with start_ymd skipped; conflict check behind
check_namelist_opts_conflicts in process_namelist_infile, enabled only on the
user-infile path; finidat/nrevsn skipped), the new failtest
(namelist_opts_infile_conflict) with fixture, and the before/after evidence
(silent exit 0 → fatal_error naming mksrf_lsmlon; control runs green).

**Maintainer Feedback:**

- [2026.23.11]: None yet

- [2026.23.11]: PR just opened, so no maintainer review/response yet. 

**Status:** Awaiting review. 

**Toolkit**

- Tool: ship-manifest checks + the red/green suite pair, evidence in test_evidence.md.
- What it produced: failtest red on unmodified master with CSMDATA set (not ok —
  the earlier "ok" was a false pass from the Yellowstone default inputdata path,
  caught and documented), rehearsal flipped from silent exit 0 to the fatal_error
  naming mksrf_lsmlon, both no-conflict controls stayed exit 0, and the green run
  showed ok with no new failures vs. the documented Windows baseline.
- Difficulties: 3425 tests × ~1 hour per run on Windows; grep refused the binary-ish
  output until -a; the suite and any manual rehearsal share the working directory
  and can't run concurrently.
- What changed: all suite invocations now carry CSMDATA=/tmp/inputdata, and the
  baseline-exit-254 quirk is recorded in ship-manifest.md instead of being fought.

---

## Learnings and Reflections

**Technical Skills Gained**

Perl in a 6000-line production module — reading `CLMBuildNamelist.pm`'s merge
order and the `Build::Namelist` API (get_group_names/get_variable_names) well
enough to add a parameter-threaded check without touching shared CIME code.
Test-first on an unfamiliar harness: writing a data-driven failtest entry in
build-namelist_test.pl from existing entries' shape. Windows reality under
Git Bash: process names, MSYS path mapping, python launcher stubs, and what
"the hook ran" actually requires verifying.

**Challenges Overcome**
The silent ship-gate (four stacked causes: stale sessions, python3 stub,
PowerShell-vs-Bash matcher, and the tool_name gate inside the course scripts
themselves) — diagnosed layer by layer with canary hooks and payload logging,
then fixed and reported. The false-pass suite run — my "red" test passed for
the wrong reason until I traced the Yellowstone default inputdata path.
And plan-check's honest-uncertainty rejection, which forced me to delete an
argument I liked but couldn't verify — the plan that survived it is the one
my merged fix was built from.

**What I'd Do Differently Next Time**

- Verify the gate before trusting it: A canary hook and one deliberate
outgoing-command test on day one would have saved me a week of testing. 
- Diff suite output against a stored baseline file instead of eyeballing before/after logs.
- Write the repro as a runnable script from the start rather than
reconstructing it from terminal history.

---

## Resources Used

- ESCOMP/CTSM#2256 — the issue thread itself: the maintainer's spec
  ("change one or the other") and scope carve-outs defined the fix; my claim
  comment (#issuecomment-6869064418) and repro comment
  (#issuecomment-7086475038) live there.
- The repo's own harness: bld/unit_testers/build-namelist_test.pl supplied
  the failtest pattern, make_config_cache/make_env_run fixtures, and the
  clmexp variable candidates from namelist_definition_ctsm.xml.
- Claude Code documentation and the course's INSTALL.md/ship-gate materials
  for the hook wiring that the Windows bugs were measured against.