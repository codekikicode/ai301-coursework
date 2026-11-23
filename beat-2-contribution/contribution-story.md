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
**Pull Request:** [to be opened in Unit 7/8]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

````
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
````

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built my issue-scout, then rebuilt its rubric twice to choose my issue**

I installed the issue-scout over my unit-1 issue-select, wrote my fit profile, and built a search strategy from two gh search issues queries with ranking filters. My scan graded five candidates with four accepts (all from one repo, srtab/daiv — zero diversity), but TF Jacob Cho directed me to pick from the AI301 Issue Selection site. There my v1 rubric rejected everything real; so I loosened three checks (60-day staleness windows for claims and PRs, clearer spec bar). When the scout then flagged its own inconsistency — a stale-assignee case on OpenSearch #4253 — I patched that too (v3). It still rejected that issue on new evidence, which told me the tool was working, not just permissive. My final picks graded: CTSM#2256 accepted 10/10, django-rusty-templates#27 rejected (AI policy bans LLM help on good-first-issues plus a fresh claim). I chose CTSM#2256.

**Unit 6:  Installed the voice guard, re-scoped repro-check and plan-check for the wild, and wrote the repo memory file**

The voice guard fought me three times before it fired: MSYS ln -s made silent copies instead of symlinks (fixed with the pointer-file fallback), my machine had no Python at all so the hook's python3 call could never have worked (installed 3.12, rewrote the hook to python + absolute path), and the first wiring test ran unblocked because my Claude session predated the settings edit. Then a subtler one: the guard's checker can't launch npm's claude.CMD on Windows (subprocess with shell=False), so I installed the native claude.exe build — reported in #dts-fa26-ai301-build-support. The memory file paid off immediately: orienting bld/ surfaced the test gap (no test sets the same variable in both -namelist and -infile), which is where my fix's test will go.

**Unit 7: Installed the ship-gate and fought Windows for a week to make it fire**

The installer wrote my ship-manifest (3 checks: validate_xml.py passes; the Perl namelist test driver fails on unmodified master on my machine — exit 254, a platform quirk I documented rather than hid; Python tests blocked, no conda). Then the hook saga: the gate silently never ran because (1) the hook called python3, which is a broken Microsoft Store stub on this box, (2) the matcher said Bash but my Claude Code's shell tool is literally named PowerShell (and Bash|PowerShell alternation doesn't match), and (3) the course scripts themselves gated on tool_name != "Bash" — I patched both scripts to accept ("Bash", "PowerShell") and reported all three bugs in #dts-fa26-ai301-build-support. Verified live: ship-gate STOPs a gh pr create.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

A second, independent repro (use_c13, run from bld/unit_testers) was posted to the issue thread: [link]" — or swap one to match the other.

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

**Analysis**
`CLM_NAMELIST_OPTS` and `user_nl_clm` enter through `cime_config/buildnml` as the `-namelist` and `-infile` arguments to `bld/build-namelist`. In `CLMBuildNamelist.pm`, `process_namelist_user_input` (line 594) calls `process_namelist_commandline_namelist` (line 1524) first, then `process_namelist_commandline_infile` (line 1575), which calls `process_namelist_infile` (line 1547).

Both merge via `Build::Namelist::merge_nl` (`cime/utils/perl5lib/Build/Namelist.pm:373`), which is first-write-wins: variables already set are silently skipped. So any item set in both places keeps the `CLM_NAMELIST_OPTS` value and the user's `user_nl_clm` edit is silently discarded — exactly the behavior described in the issue. The issue asks for a clear "change one or the other" message when a setting appears in both `CLM_NAMELIST_OPTS` and `user_nl_clm`, so the check belongs in `CLMBuildNamelist.pm`.

`Build::Namelist::merge_nl` has a `die_on_conflict` option, and `process_namelist_infile` already passes `die_on_conflict =&gt; 1` for one call — but it can't be the whole fix. Its error message is generic ("A variable was already set...") and doesn't name `CLM_NAMELIST_OPTS` or `user_nl_clm`, which is exactly the clear message the issue asks for. (I initially suspected a conflict risk across multiple sequential infiles, but `cime_config/buildnml:382` passes a single combined `-infile`, so I dropped that argument rather than assert it unverified.)

Two risks to design around, both from `cime_config/buildnml` injecting content the user didn't write: (1) it always adds `start_ymd=&lt;RUN_STARTDATE&gt;` to the `-namelist` string alongside `CLM_NAMELIST_OPTS` (~line 382), so `start_ymd` must be skipped when recording `-namelist` variables; (2) for branch/hybrid runs it writes `finidat`/`nrevsn` lines into the combined infile (~line 367), so those are skipped in the comparison too. Known trade-off: a user who genuinely sets `finidat` in both `CLM_NAMELIST_OPTS` and `user_nl_clm` won't get the error — accepted, since a false blame is worse than a missed one.

The check lives in `process_namelist_infile` (where `$nl_infile_valid` already exists), behind a new option — e.g. `check_namelist_opts_conflicts =&gt; 1` — that only `process_namelist_commandline_infile` passes. The CAM `drv_flds_in` call at line 4390 doesn't pass the flag, so it's unaffected.

I reproduced this on master (`5e1da3a`): with `use_c13=.true.` passed via `-namelist` (what `CLM_NAMELIST_OPTS` maps to) and `use_c13=.false.` in the `-infile` (what `user_nl_clm` maps to), `build-namelist` completed with no error or warning, and the generated `lnd_in` contained `use_c13 = .true.` — the infile value was silently discarded. Repro details posted in this comment: https://github.com/ESCOMP/CTSM/issues/2256#issuecomment-7086475038

**Proposed Solution**
- In `process_namelist_commandline_namelist`, record the set of variables (group + name) that the `-namelist` pass set (e.g. into `$nl_flags`), skipping known buildnml-injected variables such as `start_ymd`.
- In `process_namelist_commandline_infile` (1575 — which handles only user `-infile` arguments), pass a new `check_namelist_opts_conflicts => 1` option to `process_namelist_infile`. There, before merging each user infile, enumerate `$nl_infile_valid` with `get_group_names`/`get_variable_names`/`get_variable_value`, collect any variables present in the recorded set (skipping `finidat`/`nrevsn`), and if the list is non-empty, `$log->fatal_error` naming every duplicated variable and telling the user to remove the setting from either `CLM_NAMELIST_OPTS` or `user_nl_clm` — per the issue text.
- Out of scope, per the issue: duplicates within `user_nl` files, and no change to `merge_nl` itself (shared CIME code).

**Implementation Plan**
- Branch `fix/2256-namelist-opts-conflict` (or per CTSM convention).
- Add the variable-set recording in `process_namelist_commandline_namelist` and the duplicate check in `process_namelist_infile` behind the new flag, passed only from `process_namelist_commandline_infile`.
- Add a test to `bld/unit_testers/build-namelist_test.pl` that passes both a `-namelist` fragment and an infile setting the same variable, and asserts the death — using the existing fixture files (`myuser_nl_clm`/`empty_user_nl_clm`) as a model. Verify it fails without the fix, passes with it.
- Run manifest checks (XML validation) and the reproduction steps; capture before/after output in `test_evidence.md`.

**Toolkit**

- Tool: plan-check (wild-scoped), run three times against plan.md + plan-comment.md.
- What it produced: reject (no posted repro evidence) → reject (honest-uncertainty: my  plan contradicted itself — first-write-wins can't coexist with "later files override earlier ones") → accept, after it verified my code claims against the repo live and caught two real design risks I'd missed (start_ymd injected into -namelist, finidat/nrevsn into the infile).
- Difficulties: it read the actual CTSM source to check my claims — I couldn't hand-wave. It also ruled my plan-comment stays off the thread until a maintainer replies.
- What changed: posted a standalone repro comment; dropped the unverifiable multi-infile argument and said so openly; moved the check behind a flag so CAM's drv_flds_in call is unaffected; added skip-lists for buildnml-injected variables.
---

## Testing Strategy

Repro re-run (before/after): the exact steps in Reproduction Process, on my fix branch. Before: exit 0, silent, -namelist value wins. After (pass criteria): build-namelist dies non-zero, message names the duplicated variable(s) and says to remove the setting from CLM_NAMELIST_OPTS or user_nl_clm.

Control re-run: variable only in user_nl_clm must still be honored (no false positive), and a conflict-free run must produce identical lnd_in to before.
New unit test in bld/unit_testers/build-namelist_test.pl: same variable via -namelist and -infile, asserts death. Verified failing without the fix, passing with it.
Manifest checks: python .github/workflows/validate_xml.py must pass. The full Perl suite is run as a before/after diff, since its baseline on Windows already fails (exit 254 — documented in ship-manifest.md); the criterion is "no new failures beyond baseline."

All output captured in test_evidence.md.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

**[2026-11-23]**

Plan accepted by plan-check on the third run. Key design decisions locked: check lives in process_namelist_infile behind a new check_namelist_opts_conflicts => 1 flag passed only by process_namelist_commandline_infile (keeps CAM's drv_flds_in call at line 4390 unaffected); start_ymd skipped on the -namelist side and finidat/nrevsn on the infile side because buildnml injects those itself. Wrong turn recorded: my first plan rejected die_on_conflict with a "later files override earlier ones" argument that contradicts first-write-wins — plan-check caught it against buildnml:382

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
