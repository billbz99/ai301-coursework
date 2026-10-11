# Procedure: how this tool grades a PR package

## Read order

In eval mode every source below is a section of the bundle. In live mode the source is named in brackets.

1. Read the issue context: the title, the body excerpt, and the thread highlights. Note the symptom the issue names and any explicit maintainer direction (a requested approach, a constraint, a request to wait). [Live: the issue thread, via the URL in the request.]
2. Read the repo-facts block. List the PR template's sections, the checks the template asks the contributor to run, and the stated AI-use policy. [Live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and any AI policy file.]
3. Read the plan-context block before the PR. Note the plan's files, its in-scope and not-in-scope lines, its test plan (the command and the expected result), its deviation notes, and the repro steps it builds on. Reading the plan first means the diff is judged against what was promised, not against the PR's own framing. [Live: `plan.md`, including `## Deviations`.]
4. Read the PR title and description. Write each claim as a numbered line: what changed, what was tested, what was left out, and the issue number after "Closes". [Live: `pr_draft.md`.]
5. Read the commit list. Note any commit whose message names something the plan does not. [Live: `git log main..HEAD --oneline`.]
6. Read the unified diff. List every changed file, and write one phrase for what each hunk does. [Live: `git diff main...HEAD`.]
7. Read the test evidence last. List each command shown, and whether printed output appears under it. [Live: `test_evidence.md`.]

## Evidence gathering

1. For plan-fidelity: put the changed-file list from step 6 next to the plan's files and scope from step 3. Mark each changed file as in-plan, in a deviation note, or neither. Then mark each change the plan names as present in the diff or absent. For each absent change, record whether the description or a deviation note discloses it.
2. For description-matches-diff: for each numbered claim from step 4, find the diff line or test-evidence line that backs it, and record the claim next to that proof or next to "no proof". A claim that something was not added is backed if no hunk adds it. Do not record a routine-hygiene claim (code formatted, lint clean) as "no proof" when nothing in the package contradicts it, and do not record a main claim as "no proof" over a small imprecision in a count or a list.
3. For test-evidence-observable: copy the command and expected result from the plan's test plan. Find that command, or the reproduction's command, in the test evidence. Record whether a concrete result (printed output, or a specific stated observation such as the exact error text or "no error") is shown for the before, for the after, or for neither, and whether the after result matches the expected result.
4. For repo-checks-run: for each check listed in step 2, find its result in the test evidence or the description. Record "result shown" (printed output, or a plainly stated result such as a pass count or "clean"), "disclosed as not run, with reason", or "missing". Record every Testing box that is ticked with no result behind it.
5. For diff-reviewable: scan every hunk from step 6 for debug prints, commented-out code, dead code, formatting-only changes, and edits unrelated to the stated change. Record each with its file.
6. For standards-and-disclosure: list the template sections from step 2 and mark each as real content, empty, or placeholder text. Find where the description discloses AI use. Compare the diff and description against any maintainer direction noted in step 1.

## Check execution

1. Run the checks in the order they appear in the rubric table.
2. Grade each check only from the evidence you gathered for it, using the rubric's pass condition. Use nothing beyond the package text: in eval mode the bundle is the whole world.
3. Grade pass when the pass condition is met and fail when it is not. Grade unclear only when the package lacks the part the check reads (for example, there is no test evidence section at all). Do not grade unclear because the judgment is hard: decide from the evidence you have.
4. Re-read the diff text before grading plan-fidelity, description-matches-diff, and diff-reviewable. The other checks may be graded from your gathered notes.
5. When a shortfall is disclosed in the description or in a deviation note, apply the rubric's wording on disclosure for that check instead of failing it.
6. Grade the thing itself, never its shape: do not reward or penalize length, headings, or tone.
7. For every check, write one evidence line that names the specific fact or quote that decided it.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every check passes, and reject if any check fails.
2. Count every unclear grade as a fail.
3. When more than one check failed, quote the evidence line of the first failing check in rubric order as the deciding check in your summary.
4. Write the one-line-per-check summary, then end the reply with the JSON block from SKILL.md. The same grades must always produce the same verdict.
