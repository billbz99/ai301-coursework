# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:** In the repro report, the part that records OS, language or runtime version, the project's commit or release, and how it was installed. The issue's stated target is in the issue context and the repo-facts block. In live mode, it is in the draft report and the issue thread.

**What good looks like:** The versions named match what the issue targets, or the report says where they differ. "Latest" or "my laptop" with no version is not a record.

## Steps

**Where it lives:** In the repro report, the commands and actions listed between the starting state and the moment the behavior appears. In live mode, the draft report.

**What good looks like:** Every command is written out literally, and anything the trigger depends on (an install, a fixture, an input file) is included. A stranger could run them in order from a fresh clone and reach the trigger.

## Behavior shown

**Where it lives:** In the repro report, the output excerpts, logs, or screenshots, compared with the error or wrong behavior in the issue's title, body, and thread highlights. In live mode, the pasted output in the draft.

**What good looks like:** The artifact shows the issue's own symptom: the same error type and message, failing test, or wrong value. A different error, or an error from an earlier step, is an adjacent behavior and does not count.

## Honesty

**Where it lives:** Where the report's stated outcome ("reproduced" or "could not reproduce") meets the artifacts that follow it.

**What good looks like:** The claim matches the evidence exactly. An honest cannot-reproduce that shows what was tried and the versions used is a good report. A confident "reproduced" backed by a different behavior, or a root-cause claim with no evidence, is not.

## Comms

**Where it lives:** In the claim comment and the repro report, compared with the repo-facts block: the bug-report template asks and the contribution policy, including any AI-use disclosure rule. In live mode, the repo's CONTRIBUTING file and issue or PR templates.

**What good looks like:** The substance the template asks for (version, minimal reproduction steps) is present; a missing "I searched for duplicates" confirmation is not a failure. Where the policy requires disclosing AI assistance, the comments say so. The claim names the issue's specifics and promises only an investigation, never a fix or a date. If the repo says nothing, nothing extra is required.

