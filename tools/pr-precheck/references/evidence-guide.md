# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:** In an eval bundle, the plan-context block holds the plan's scope pair (what is in scope and what is not), the files it names, and any deviation notes. The candidate PR section holds the unified diff, the commit list, and the title and description. In live mode, the plan is `plan.md` and its `## Deviations` section, the diff comes from `git diff main...HEAD`, and the description is the body of `pr_draft.md`.

**What good looks like:** Every changed file falls inside the plan's stated files or scope, or is named in a deviation note, and every change the plan promised is in the diff, or its absence is disclosed. Silent drift runs in two directions: the diff does more than the plan (an unnamed file or hunk), or less with no note. A description that claims more or less than the diff delivers is drift too: each claim in it has a line in the diff behind it.

## Test evidence (harness category: not-tested)

**Where it lives:** In an eval bundle, the candidate PR's test-evidence section, read against the plan-context block's test plan and the repro steps, and against the checks the repo-facts block's PR template lists. In live mode, `test_evidence.md`, read against `plan.md`'s test plan and `.github/PULL_REQUEST_TEMPLATE.md`.

**What good looks like:** The evidence shows the command from the plan's test plan and the concrete result observed before and after the change: printed output, or a specific stated observation such as the exact error text, the rows listed, or "no error". The after result matches what the plan said to expect. Each check the template or the contribution guide lists is reported with its result (printed output, or a plainly stated result such as a pass count or "clean"), or the description says honestly which check was not run or failed and why. A general sentence saying "tests pass" or "it works", with no concrete before or after result, proves nothing.

## Diff quality (harness category: unreviewable)

**Where it lives:** In an eval bundle, the unified diff and the commit list in the candidate PR section. In live mode, `git diff main...HEAD` and `git log main..HEAD --oneline`.

**What good looks like:** The fix is visible, and every hunk serves the stated change. The debris tells are debug prints, commented-out blocks, dead code, formatting-only churn, and drive-by edits to code the issue does not mention. A diff can have debris inside a file the plan names, so check hunks and not only file names.

## Standards and comms (harness category: standards-wall)

**Where it lives:** In an eval bundle, the repo-facts block states the PR template's sections, the contribution asks, and any AI-use policy, and the thread highlights show explicit maintainer direction. The candidate PR's description is read against them. In live mode, the template is `.github/PULL_REQUEST_TEMPLATE.md`, the policy is in `docs/CONTRIBUTING.md` or any AI policy file, the direction is in the issue thread, and the description is `pr_draft.md`.

**What good looks like:** Every ask the repo-facts block lists is met in the description or the diff: an entry the template requires (a changelog or whatsnew line) appears in the diff, each template section has real content, the issue is named by number, and each check the template lists is reported. Where the repo's stated policy requires AI disclosure, the description makes it; if the repo states no AI policy, a missing disclosure is not a failure. The diff and description do not contradict maintainer direction in the thread. Compliant text is specific to this PR; a section left as template placeholder, an unmet template ask, or a missing disclosure the policy requires is a visibly ignored ask. Whether the description's claims match the diff belongs under plan fidelity, above.
