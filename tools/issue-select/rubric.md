## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Community alive: maintainers respond | Comment thread + repo-facts ("last 5 default-branch commits", "maintainer first-response sample") | A human maintainer/collaborator has committed, merged, or first-responded within 12 months before the capture date. Bot-only commits do not count by themselves; a bot merging a human's PR does | required |
| Repo in use | Repo-facts ("latest release", "last push", "archived:", stars) | The repo is NOT archived, AND (a release shipped within 18 months before the capture date OR the repo shows real adoption: substantial stars or dependents) | required |
| Allowed to contribute: policy | Repo-facts "contribution policy" line | No outright ban on AI-generated contributions. Conditions (disclose AI use, understand/test changes, human review) pass; silence passes | required |
| Scope: one bounded change | Issue body + thread | One bounded piece of work. Fails if it is an umbrella/tracking issue, the design is still openly debated with no maintainer settling it, a maintainer says it touches core internals, or it is a usage/support question | required |
| Scope: spec included | Issue body | A concrete spec — expected behavior, repro steps, or acceptance criteria a fix can be verified against. A terse body or checklist still passes if the work itself is bounded | required |
| Unclaimed: no assignee | "this issue: assignees:" in repo-facts | No assignee listed | required |
| Unclaimed: no open PR | "linked PRs:" plus PRs mentioned in the thread | No open pull request linked to or mentioning this issue as fixed. When sidebar and thread disagree, believe the thread | required |
| Unclaimed: no fresh claim | Comments section | No recent comment from a maintainer or outside contributor asserting they are actively working on it. Path Review house rule: classmates' claim comments never count as claims and must be ignored for this check | required |
| Newcomer-friendly wording | Issue body | Clear title, self-contained context, no required insider knowledge | preferred |
| Maintained recently | Repo-facts | Maintainer activity within 3 months before the capture date | preferred |

## Verdict rule

Only accept if every **required** check passes. Any required check graded `fail` or `unclear` → reject (`unclear` is treated as `fail`: an unverifiable issue is not a first issue you should take). Preferred checks never affect the verdict; they only rank accepted issues.