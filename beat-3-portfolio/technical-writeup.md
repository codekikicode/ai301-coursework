# Catching a silent bug in a climate model's build system — and making it loud

## Overview

CTSM (the Community Terrestrial Systems Model) builds its configuration from a
Perl tool called build-namelist. Users can set the same option in two places —
an environment variable (CLM_NAMELIST_OPTS) and a config file (user_nl_clm) —
and when they collide, one silently wins. The user thinks they changed
something; they didn't. I reproduced the behavior on current master, designed a
fix with a planning tool that graded my plan against the real source, added a
regression test that fails without the fix, and opened https://github.com/ESCOMP/CTSM/pull/4344. 

It stands today as an open PR with
passing CI; the judgment parts I brought myself were my scout's rubric for
choosing the issue, my ship-gate manifest defining "shippable," and the plan
plan-check graded three times.

## What happened

I found ESCOMP/CTSM#2256 through an issue-scout I'd built and re-tuned twice
after it rejected everything real or accepted a stale-assignee case it flagged
on itself. The issue was unusually well-specified — "die with a clear error
when an item is set in both places" — but the codebase was not: a 6200-line
Perl module where both inputs merge in order, first-write-wins, no duplicate
detection anywhere.

Reproduction came before any code. With a hand-built config stub I ran the
exact command the test suite later automated:

    ../build-namelist ... -namelist "&clmexp mksrf_lsmlon=96 /" \
        -infile namelist_opts_conflict_user_nl_clm
    exit: 0        # silent: the -namelist value wins, nothing said

That exit 0 with no output is the entire bug. I posted this reproduction to the
issue thread as evidence.

Then a planning tool, plan-check, rejected my plan twice. The second rejection
mattered most: I had argued against an existing code path with a claim —
"later files intentionally override earlier ones" — that directly contradicted
the first-write-wins merge I'd described two paragraphs earlier. plan-check
verified it against the live repo: buildnml passes one combined infile, so my
argument had no ground. Verdict block, quoted:

    honest-uncertainty: fail. States merge_nl is "first-write-wins" yet
    asserts "later files intentionally override earlier ones"...
    buildnml passes a single combined -infile.

I deleted the argument instead of defending it, and the plan was accepted on
the third run. It also found two real design traps I had missed: buildnml
injects start_ymd into the option string and finidat/nrevsn into the file, so a
naive duplicate check would blame users for conflicts they didn't create.

The test-first loop had one wrong turn worth keeping: my new test initially
"passed" on unmodified master — a false pass, because the suite's default
inputdata path is a Yellowstone cluster directory that doesn't exist on my
machine, and the process died on an environment check before reaching the code
under test. Any early death satisfies a failtest's "must die" assertion. With
CSMDATA pointed at a real directory, the truth appeared:

    Before fix: namelist_opts_infile_conflict ... exit 0, silent
    After fix:
    ERROR : ...process_namelist_infile() :
    The following namelist item(s) are set in BOTH CLM_NAMELIST_OPTS and user_nl_clm:
      mksrf_lsmlon (in group &clmexp)
    Remove the setting from one or the other ...
    exit: 255

Full suite after the fix: my test `ok 1107`, failure count unchanged at 1052 —
identical to the unmodified-master baseline (pre-existing Windows platform
failures, documented rather than hidden).

## Limitations and what's next

The edge I chose to accept: a user who genuinely sets finidat in both places on
a branch/hybrid run won't get the error, because buildnml-injected finidat is
indistinguishable from a user-supplied one on the file side — a false blame
seemed worse than a missed conflict, and the trade-off is written in the PR.

Next, I'd close the false-pass class entirely: the suite's default inputdata
root silently invalidates its failtests on any machine outside NCAR, which cost
me one debugging round and could cost a future contributor their confidence in
a green run. A one-line default fix or a startup warning would do it — and
it's a follow-up issue I'd happily write.

The PR remains open as of this writing; silence is normal for this repository,
and my monitoring playbook says the right move today is no move.