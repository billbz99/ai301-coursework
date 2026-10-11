# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context first: the title, the body excerpt, and the thread highlights. Note the symptom the issue names and any maintainer signal (a request to wait, a settled design, a requested approach).
2. Read the repo-facts block. Note the stated bug-report or plan template asks, the contribution asks, and any AI-use policy.
3. Read the repro-evidence block before the plan. Note the exact command, the environment, and the artifact (the error, value, or output) it shows. Reading the evidence before the plan means the plan's cause is judged against the evidence, not against the plan's own framing.
4. Read the candidate plan. Note its stated cause, its scope statement and not-in-scope line, the files it names, its approach, its test plan, and its risks and unknowns.
5. Read the candidate plan comment last. Note what it says about the diagnosis, scope, and test, and whether it promises anything.

## Evidence gathering

1. For diagnosis-grounded and targets-cause: copy down the artifact line from the repro evidence (the error or wrong value), then copy down the plan's cause sentence and its approach sentence.
2. For scope-bounded: list every file and change the plan names. Next to each, write whether the stated cause needs it.
3. For executable: write down, for each named file or function, what the plan says changes in it. If the plan names no file or function, write "none named".
4. For test-observable: copy down the repro command from the repro evidence and the plan's expected result after the fix. If no expected result is stated, write "none stated".
5. For unknowns-honest: copy down every claim of certainty in the plan and every unknown or risk it lists.
6. For comment-fits-thread and comment-specific: copy down the maintainer signals from the thread, the repo's stated asks and AI-use policy, and the comment's diagnosis, scope, test, and any promise.

## Check execution

1. Run the checks in the order they appear in the rubric table.
2. Grade each check only from the evidence you gathered for it, using the rubric's pass condition. Do not use knowledge of the real repository or issue beyond the package text. The package is the whole world.
3. Grade P if the pass condition is met and F if it is not met. Grade unclear only when the package does not contain the part the check reads (for example no repro-evidence block). Do not grade unclear because the judgment is hard: decide from the evidence you have.
4. Grade what the plan says and shows, never its shape. Do not penalize length, formatting, headings, or tone, and do not reward them.
5. A check may be graded from the notes you gathered, without re-reading the whole package, except diagnosis-grounded and targets-cause: re-read the repro artifact against the plan's cause before grading those two.
6. For each check, write one line of evidence naming the specific text that decided it.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every check is P. Any F means reject.
2. Count each unclear grade as a fail, as the verdict rule says.
3. In the output, quote the evidence line for the check that decided a reject. If several checks failed, quote the first failing check in table order.
4. End the output with the JSON block whose verdict is accept or reject. The same grades must always produce the same verdict.