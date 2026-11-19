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

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

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

- Tool:
- What it produced:
- Difficulties:
- What changed:

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

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

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
