# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

\---

## Your identity upstream

**GitHub username**

billbz99

\---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-6030508593

Hi, I'd like to take this one. The test `test\_readme\_with\_all\_quality\_signals` in `tests/unit/test\_readme\_scorer.py` is marked xfail because its README fixture is shorter than its own `word\_count > 100` assertion. I'll reproduce it locally and report back with the exact output, plus what I find about whether the fixture or the assertion should change.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-6030657302

**Environment:** Windows 11 Pro, Python 3.14.6, pytest 9.1.1. Commit f89c06f of main (my fork of codepath/pathreview-ai301-fa26-s1). Installed in a venv with `pip install -e ".\[dev]"`. I skipped Docker and `make setup` because the unit tests don't use the services.

**Steps:**

```
git clone https://github.com/billbz99/pathreview-ai301-fa26-s1.git
cd pathreview-ai301-fa26-s1
python -m venv .venv
.\\.venv\\Scripts\\pip install -e ".\[dev]"
.\\.venv\\Scripts\\pytest tests/unit/test\_readme\_scorer.py -v --runxfail
```

**Output:**

```
>       assert data\["word\_count"] > 100
E       assert 51 > 100
tests\\unit\\test\_readme\_scorer.py:60: AssertionError
readme\_scored  category=minimal score=0.8717142857142858 word\_count=51
FAILED tests/unit/test\_readme\_scorer.py::TestReadmeScorer::test\_readme\_with\_all\_quality\_signals - assert 51 > 100
1 failed, 22 passed in 0.83s
```

Without `--runxfail` the same test shows as XFAIL (22 passed, 1 xfailed).

**Observed:** the fixture scores a word\_count of 51, so the `word\_count > 100` assertion fails on line 60, before the later assertions run. I haven't yet looked at whether the fixture or the assertion should change.

I ran these commands myself; the output above is from my machine.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `python run\_eval.py --rubric ... --evidence ... --limit 3` (partial, first version of my rubric): "agreement: 2/3 scored items". pkg-01 was rejected with the note "failed: conventions-followed".
2. `python run\_eval.py ... --only pkg-01,pkg-03,pkg-07,pkg-19,pkg-20` (partial, after rewriting conventions-followed and making claim-specific required): "agreement: 5/5 scored items".
3. `python run\_eval.py ... --save-run eval-run.txt` (full run): "agreement: 18/20 scored items  (bar: 18/20: PASS)". The two misses were pkg-05 and pkg-12, both "failed: steps-followable".

The last score, 18/20, matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

pkg-01 (httpie/cli#1640). My first version of the rubric decided reject; the gold label is accept. The gold note reads: "faithful offline repro of the missing Content-Type with a control run; env recorded; claim specific and modest". The harness note on my `--limit 3` run read "failed: conventions-followed".

The package's repo facts say: "bug reports: template asks reporters to confirm they searched for similar issues and are on the latest version, and to provide minimal reproduction steps". My first pass condition failed any package where a template ask was absent. The report never says the author searched for similar issues, so my check failed it, even though the report records "HTTPie 3.2.4 (pip), Python 3.12.4" and gives exact commands with a control run. I had read the template's confirmation sentence as a requirement, when the substance it asks for (the version and minimal reproduction steps) was present. I rewrote the check to grade that substance and not the confirmation sentence. With the rewritten rubric pkg-01 agrees (accept / accept) in the later runs.

**Check rationale**

conventions-followed, as it reads in my uploaded `rubric.md`:

"Pass if the report gives the substance the template asks for (the version in use and minimal reproduction steps) and, where the policy requires disclosing AI assistance, the comments contain that disclosure. Treat every package as AI-assisted work, so a repo policy that requires disclosure applies to it. Fail if the policy requires disclosure and the comments do not disclose, or if a substantive ask (version, reproduction steps) is missing. Do not fail a package for lacking a confirmation sentence such as "I searched for similar issues". If the repo states nothing, or its policy needs no disclosure, pass."

It reads that way for two reasons. The sentence "Do not fail a package for lacking a confirmation sentence" came from the pkg-01 miss above: my first version failed a faithful repro over boilerplate. The sentence "Treat every package as AI-assisted work" was added because the gold note for pkg-20 says "course packages are treated as AI-assisted work", and a grader that assumed a human author could pass a package that breaks a disclosure policy. I rejected a looser version that only checked for a bug template, because the set has a one-package disclosure category.

**Trade-offs**

This check gives up catching packages that skip a template's confirmation line, such as the "I searched for similar issues" item in the repo template for pkg-01. A maintainer might still want that line, and my rubric will not hold a package for it.

Because that change loosened the check, I re-ran canaries with `--only` before the confirming full run: pkg-03 and pkg-07 (accepts that had to stay accepts) and pkg-20 (the disclosure package that had to stay a reject), along with pkg-01 and pkg-19. All five agreed ("agreement: 5/5 scored items"), and the full run then kept the disclosure category matched ("disclosure 1/1").

\---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

