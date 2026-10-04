# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Repo facts: the last 5 default-branch commits (dates and author names), measured against the capture date stamped at the top of the bundle | At least 1 of the last 5 commits is human-authored (author name does not end in [bot]) and dated within 90 days before the capture date. Fail if all 5 are bots or the newest human commit is older than 90 days. | required |
| repo-in-use | Repo facts: the archived flag, the latest release date, and the last push to any branch | archived is false AND (latest release or last push is within 180 days before the capture date). Fail if archived is true, or if both the latest release and the last push are older than 180 days. | required |
| unclaimed | Repo facts: this issue's assignees and linked PRs (with state); the Comments section for claim phrases ("I'll take this", "can I work on this", "working on this") and PRs mentioned in comments | Pass only if ALL are true: assignees is none; no linked or mentioned PR is open; no comment claiming the issue is dated within 60 days before the capture date. If the sidebar facts and the thread disagree, believe the thread. A closed, unmerged PR (an abandoned attempt) does not fail this check by itself. | required |
| scope-bounded | Issue title and body, plus the Comments section | Pass if the issue asks for one bounded piece of work. Fail if ANY is true: it is an umbrella or tracking issue (a list of sub-items to split into separate work); a maintainer says the fix needs changes to core internals; the thread shows the design is still being debated with no maintainer decision; or it is a usage or support question rather than a change request. A short body, an acceptance-criteria checklist, or a bug report without reproduction steps is NOT a fail. | required |
| ai-policy-allows | Repo facts: the contribution policy line (CONTRIBUTING.md, AI_POLICY files, templates) | Fail only if the policy outright bans AI-generated or AI-assisted contributions. Disclosure, personal-understanding, testing, or human-review requirements are conditions, not bans: pass. If the policy line says nothing about AI, pass. | required |
| good-first-label | The issue's labels | Has a good first issue (or equivalent, such as beginner or help wanted) label. | preferred |
| maintainer-responsive | Repo facts: the maintainer first-response sample | The sampled first replies from Owner, Member, or Collaborator came within 14 days. | preferred |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. A grade of unclear on a required check counts as a fail. Preferred checks never change the verdict; they are used only to rank accepted issues (more preferred checks passed ranks higher).