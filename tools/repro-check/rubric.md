\# Rubric: is this reproduction package ready to post?



\## Checks



| Check | Evidence | Pass condition | Weight |

|---|---|---|---|

| environment-recorded | The repro report's environment record (OS, language or runtime version, project version or commit, how it was installed), read against the version or target the issue names and the repo-facts block | Pass if the report names the runtime version and the project commit or release it ran on, and that matches what the issue targets or the difference is called out. Fail if the environment is missing, vague ("my machine", "latest"), or silently differs from the issue's stated target. | required |

| steps-followable | The repro report's commands and actions, read from the starting state to the point where the behavior appears | Pass if a stranger starting from a fresh clone could reach the trigger: each command or input is given literally and every setup the trigger depends on is included. Fail if a needed command, file, input, or setup step is missing or replaced by a gesture ("do the usual setup"), so the trigger cannot be reached. Do not grade length or formatting. | required |

| behavior-matches-issue | The output excerpt, log, or screenshot in the repro report, read against the error or wrong behavior the issue describes | Pass if the artifact shows the same symptom the issue names (same error type and message, same failing test or function, same wrong value). Fail if it shows an adjacent or different failure, or if the report claims a result with no artifact shown. Unclear if an artifact is present but cannot be tied to the issue's symptom. | required |

| outcome-honest | The outcome the report states, read against what its artifacts actually show | Pass if the stated outcome is exactly what the artifacts support. An evidenced cannot-reproduce (what was tried, versions, output) passes. Fail if it claims "reproduced" on the strength of a different behavior, claims more than it shows (for example a root cause with no evidence), or says cannot-reproduce without showing what was tried. | required |

| conventions-followed | The claim comment and the repro report, read against the repo-facts block: the stated bug-report template asks and the contribution policy, including any AI-use policy | Pass if the report gives the substance the template asks for (the version in use and minimal reproduction steps) and, where the policy requires disclosing AI assistance, the comments contain that disclosure. Treat every package as AI-assisted work, so a repo policy that requires disclosure applies to it. Fail if the policy requires disclosure and the comments do not disclose, or if a substantive ask (version, reproduction steps) is missing. Do not fail a package for lacking a confirmation sentence such as "I searched for similar issues". If the repo states nothing, or its policy needs no disclosure, pass. | required |

| claim-specific | The claim comment, read against the issue | Pass if the claim names the issue's specifics (the function, file, command, or symptom) and promises only investigation. Fail if it is interchangeable boilerplate that could be pasted on any issue, a bare "+1" or "me too" with no stated intent, or if it promises a fix, a guarantee, or a date. | required |



\## Verdict rule



Ready (accept) if every check passes. Hold (reject) if any check fails. A grade of unclear on any check counts as a fail.

