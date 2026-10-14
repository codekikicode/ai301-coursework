# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:** Eval bundle: the "Plan context" block's stated scope, named files, and steps, read against the "Candidate PR" diff; the description's fidelity claims (Summary and Changes) read against
the same diff live here too — a description claiming more or less than the diff delivers is silent drift, not a comms problem. 

- Live mode:
`plan.md` including its `## Deviations` section, read against `git diff main...HEAD --stat` (the file list) and the full diff, run on your branch.

**What good looks like:**
- Every changed file falls inside the plan's stated boundary or a deviation note, and every hunk implements a step the plan names. An honest deviation re-ties a mismatch: it appears in the deviation notes or the description before the diff delivers it.

Silent drift in either direction — an extra file, a missing planned step, a description claim no hunk backs — fails without a note.

## Test evidence (harness category: not-tested)

**Where it lives:** 

- Eval bundle: the candidate PR's "Test evidence" section, read against the plan context's test plan and the reproduction's own steps, plus any checks the repo-facts block names.

- Live mode: `test_evidence.md` next to `plan.md`, read against the PR
template's Testing section and the repo's own checks (`make
test-unit`, `make test-integration`, `make lint`, `make typecheck`).

**What good looks like:** 

- Decisive evidence names an observable behavior and shows the expected-after state on the branch. Suite results may appear as specific claims (named command + outcome, like 'cargo test passes (214 tests)') rather than pasted output; 'tests pass' with no command, no outcome, and no observable repro proves nothing.

## Diff quality (harness category: unreviewable)

**Where it lives:** 

- Eval bundle: the unified diff and commit list under "Candidate PR". Live mode: the full `git diff main...HEAD` from your branch and `git log main..HEAD` for the commits.

**What good looks like:** 

- The fix is visible and nothing unrelated rides along: every hunk is on-topic for the issue, commit messages describe the change, and `--stat` lists only files the plan names. The debris tells: debug or print leftovers, commented-out blocks, dead code, formatting churn, and drive-by edits in files the issue does not touch.

## Standards and comms (harness category: standards-wall)

**Where it lives:** 

- Eval bundle: the repo-facts block's PR template sections, contributing instructions, and stated policy (including any AI-use disclosure request), read against the candidate PR's title and description — including explicit maintainer direction in the thread highlights. 

- Live mode: the issue thread, `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`, read against `pr_draft.md`'s title and description. (Whether the description's claims match the diff is plan fidelity, above — not this family.)

**What good looks like:** 

- Every stated ask is answered with real content: each required template section filled, the issue referenced
where required, the AI-use disclosure present where policy asks for one, and maintainer direction in the thread engaged rather than ignored. Compliant next to boilerplate or a visibly skipped section is the pass/fail line.