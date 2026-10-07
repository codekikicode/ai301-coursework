# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The candidate plan's stated cause, read against the repro evidence block's expected/actual behavior | Passes if the plan names a specific cause that explains the behavior the repro evidence actually shows; it must not contradict or ignore the quoted evidence, and it must fix the cause the evidence points to, not just the symptom | required |
| scope-bounded | The plan's scope statement: what it will change and what it won't | Passes if the plan names each file or area it will change AND states what it will not touch | required |
| executability | The plan's change description: files or areas named, approach, order of work | Passes if the plan names the files or areas to change and work can start without asking the author anything; a named tracing/debug method with a working setup counts for details the plan defers with a stated reason. Fails only if no files or areas are named, or the next step needs information only the author has | required |
| honest-uncertainty | The plan's risks and unknowns, read against what its own evidence shows | Passes unless the plan presents a claim as certain while its own evidence contradicts it or cannot support it AND it names no way to verify the claim. Working hypotheses grounded in quoted evidence, stated unknowns, and reasoned deferrals all pass; absence of a risks section is not a fail by itself | required |
| thread-and-conventions | The candidate plan comment, read against the thread highlights and the repo-facts block (templates, contribution policy, AI-disclosure asks) | Passes if the comment fits the maintainer's stated signals and policies — it acknowledges stated constraints instead of ignoring them | required |

## Verdict rule

accept (ready) only if every required check passes. A check graded ?
(not enough evidence to tell) counts as fail, and yields reject (hold).
The verdict space is binary.