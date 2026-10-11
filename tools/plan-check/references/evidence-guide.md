# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** The plan's stated cause is in the candidate plan. The behavior it must explain is in the repro-evidence block (the command, the environment, and the output or error), and in the issue's title and body. Live, the repro is in the student's posted repro comment and the plan is in the draft plan.md.

**What good looks like:** The stated cause explains the specific behavior the repro artifact shows, and the plan quotes or cites that evidence. A cause that explains a different error, or that nothing in the repro evidence supports, does not follow from the evidence.

## Scope

**Where it lives:** In the candidate plan: the in-scope statement, the not-in-scope line, and the files or areas it names. The issue body says what was asked for.

**What good looks like:** One bounded change tied to this issue, where every file or change named is needed by the diagnosis. A drive-by refactor, an unrelated fix, or an extra feature is scope creep.

## Executability

**Where it lives:** In the candidate plan: the files or functions it names, the approach, and the order of work.

**What good looks like:** A stranger could make the first edit without asking the author, because the plan names where to change and what changes there. "Improve the handling" names neither.

## Test plan

**Where it lives:** In the candidate plan's test plan, read against the repro-evidence block's command and artifact.

**What good looks like:** The test plan re-runs the reproduction and states the exact result that will show the fix worked. A test that would also pass before the fix, or that says only "verify it works", shows nothing.

## Honesty

**Where it lives:** In the candidate plan's risks and unknowns, read against what the repro evidence actually shows. Live, the Deviations section of plan.md records what changed during the build.

**What good looks like:** The plan states what it has not checked, and claims nothing the evidence does not show. A confident root cause with no evidence behind it, or "no side effects" with nothing to support it, is false confidence.

## Comms

**Where it lives:** In the candidate plan comment, read against the thread highlights and the repo-facts block (stated templates, contribution asks, and any AI-use policy). Live, the issue's thread and the repo's CONTRIBUTING file and templates.

**What good looks like:** The comment is consistent with what maintainers said in the thread and with the repo's stated asks, includes any disclosure the policy requires, and states this issue's diagnosis, scope, and test in its own specifics. Boilerplate that fits any issue, or a promise of a guaranteed fix or a date, is not a plan comment. If the repo and thread state nothing relevant, nothing extra is required.