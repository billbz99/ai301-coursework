# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/140

**Branch**

fix/63-readme-fixture-word-count

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `python run_eval.py --skill ... --limit 3` (partial, first version of my rubric): "agreement: 2/3 scored items". pkg-02 was rejected with the note "failed: standards-and-disclosure".
2. `python run_eval.py --skill ... --only pkg-01,pkg-02,pkg-03` (partial, after rewriting standards-and-disclosure): "agreement: 3/3 scored items".
3. `python run_eval.py --skill ... --save-run eval-run.txt` (full run): "agreement: 17/20 scored items  (bar: 18/20: below the bar)". The misses were pkg-05 ("failed: repo-checks-run"), pkg-08 ("failed: description-matches-diff, repo-checks-run") and pkg-11 ("failed: description-matches-diff, test-evidence-observable").
4. `python run_eval.py --skill ... --only pkg-05,pkg-08,pkg-11,pkg-04,pkg-07,pkg-10,pkg-14,pkg-03,pkg-12,pkg-01` (partial, after loosening three checks, with canaries): "agreement: 10/10 scored items".
5. `python run_eval.py --skill ... --save-run eval-run.txt` (full run): "agreement: 20/20 scored items  (bar: 18/20: PASS)".

The last score, 20/20, matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

pkg-05 (nushell/nushell#18848, category clear-accept). In my first full run my rubric decided reject; the gold label is accept. The harness row reads:

```
pkg-05  clear-accept    accept  reject   NO     failed: repo-checks-run
```

The package's repo facts say the contribution policy is a "standard contribution guide with formatting and test commands (cargo fmt, clippy, cargo test)". Its test evidence reports those checks in one sentence: "`cargo test -p nu-protocol` passes (312 tests); fmt and clippy clean." The harness note names only the check and not the sentence, so this is my reading of what triggered it. My first wording of repo-checks-run said "Pass if every check the template lists was run and its printed output is in the test evidence", and pkg-05 gives a pass count and "clean" but no printed output, so my check failed it. The gold label accepts it because every listed check is reported with its result and the PR's before and after for the keybinding behavior is shown in full. My check was stricter than the gold label: it demanded printed output for every listed check, when a plainly stated result is enough. I rewrote the check to accept a stated result, and in the final run pkg-05 agrees (accept / accept).

**Check rationale**

repo-checks-run, as it reads in my uploaded `rubric.md`:

"Pass if every check the template or the contribution guide lists appears in the test evidence or the description with its result (printed output, or a plainly stated result such as a pass count or "clean"), or the description honestly states which check was not run or failed and why. Fail if a listed check is never reported at all, or a Testing box is ticked for a check with no result behind it."

It reads that way because of what the 17/20 run showed. My first version asked for printed output for every listed check, and it rejected pkg-05 and pkg-08, which are gold accepts that report checks as short stated results ("fmt and clippy clean", "code formatted"). I changed "printed output" to "its result (printed output, or a plainly stated result ...)", and I added "or the contribution guide" because pkg-05's checks are listed in its contribution guide, not in its PR template. I kept the failure condition "a listed check is never reported at all" and the honest-disclosure exception, because the not-tested category exists and a PR that honestly says what it did not run can be ready. I rejected dropping the check entirely, because the same check caught a real gap in my own PR.

**Trade-offs**

This check gives up verification: it accepts a plainly stated result such as "fmt and clippy clean" without printed output behind it, so a PR could state a result it never produced and pass. I accept that, because the gold labels accept stated results and the diff and the other checks still have to match.

Because that change loosened the check, I re-ran canaries with `--only` before the confirming full run: the four not-tested packages (pkg-04, pkg-07, pkg-10, pkg-14), plus pkg-03 (silent-drift), pkg-12 (unreviewable) and pkg-01 (standards-wall), together with the three misses. All ten agreed ("agreement: 10/10 scored items"), and the final full run kept every category matched.

The check also still catches a real gap: on my own draft PR it rejected the package because black and the frontend tests that `docs/CONTRIBUTING.md` lists ("cd frontend && npm ci && npm test -- --run") were never reported. I ran them, reported the results (including one frontend failure that also fails on main), and the skill then said accept.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
