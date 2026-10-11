---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: is this ready to submit? A PR package is a candidate pull request (its title, description, commit list, unified diff, and test evidence) read against the plan it claims to implement (the plan's scope, files, test plan, and deviation notes) and the issue that plan belongs to. Never answer a different question, never grade more than one package per run, and never answer from gut feel. You answer by executing `procedure.md`, which applies the rubric in `rubric.md` to evidence found where `references/evidence-guide.md` says it lives.

## Inputs and modes

There are exactly two modes.

**Live mode** checks the student's own submission before it goes out. The inputs are:

1. `plan.md` in the top folder of the student's fork clone, including its `## Deviations` section.
2. The diff: run `git diff main...HEAD` (three dots) from the working copy. It shows everything the branch changes relative to `main`. Run `git log main..HEAD --oneline` for the commit list. Only committed changes count.
3. `pr_draft.md`: the PR title is its first line, and the description is everything under it.
4. `test_evidence.md`: the captured command output.
5. The issue, whose URL is given in the request. Gather the thread, the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`), `docs/CONTRIBUTING.md`, and any stated AI-use policy live, using `gh`, the GitHub API, or the web.

A student on the house chain reads the house plan and the house repro pack instead of their own `plan.md` and reproduction. The same checks grade the same things. Read the PR package the way a maintainer will: the package is what these inputs contain, not other files in the working directory.

**Eval mode** grades a package bundle. The bundle text is the whole world: use only what it contains, fetch nothing, and read no other file. Eval mode always grades a complete package: every check, with the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. Apply the house rules it states. Refuse to grade a pull request for any repository other than the one named on its `Repo:` line. If the `Repo:` line still contains a bracketed placeholder such as `<ORG>/<PATH-REVIEW-REPO>`, stop without grading and tell the student to fill in the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md`. Hold the outgoing PR text (the title on the first line of `pr_draft.md`, and the description under it) against each rule in the guide. In the summary, report every rule the draft breaks, quoting the rule and the offending words. The voice guide never changes the verdict on its own, because the rubric has no check that reads it. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read all three components before grading anything:

- `rubric.md` defines the checks and the verdict rule.
- `references/evidence-guide.md` maps where each kind of evidence lives, in a bundle and in live mode.
- `procedure.md` is the operating procedure. Execute it as written, in order. Where it is silent on a step, report the gap in your summary and never improvise around it.

If `rubric.md` has no checks written in it, or `procedure.md` has no steps written in it, refuse to grade, say which one is empty, and stop. Do not invent checks.

## Verdict and output

The verdict space is binary: `accept` means the PR is ready to submit, and `reject` means hold. There is no third verdict and no score. Any reservation belongs in a check's evidence line, not in the verdict.

Before the JSON block you may show a short readable summary: one line per check, plus any voice-guide notes and procedure gaps in live mode. Then end your reply with the fenced JSON block below, valid and last, with nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first. Never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish. A short, plain PR can be ready, and a long confident one can hide drift. Read the diff and the evidence against the plan, the issue, and the stated standards, never the formatting.
- The rubric decides, not you. If a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary if you want; the fix belongs in the rubric.
- The procedure decides how, not you. Follow `procedure.md` as written and report its gaps.
- An honestly disclosed shortfall is not a failure of the check it touches. A PR that says what it left out, or records a deviation from the plan, can be ready.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is silent, treat `unclear` as `fail`: a PR you cannot verify from the package is not ready to submit.
