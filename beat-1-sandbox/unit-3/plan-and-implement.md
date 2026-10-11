# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

billbz99

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-6113323391

**Plan for #63** (built from my own reproduction)

**Diagnosis:** `test_readme_with_all_quality_signals` fails at `assert data["word_count"] > 100` with `assert 51 > 100`, because its fixture README is only 51 words. Reading `agent/tools/readme_scorer.py` lines 68-73, the scorer returns "minimal" under 100 words, "adequate" under 500 and "comprehensive" otherwise, so the test's later assertion `word_count_category == "comprehensive"` needs at least 500 words. My repro stopped at the first failing assertion, so I have not yet seen the category assertion fail.

**Scope:** change only the fixture string in this one test, and remove its `xfail(strict=True)` marker. I am not changing the scorer, the assertions, or any other test.

**Approach:** extend the README fixture in `tests/unit/test_readme_scorer.py` to about 550 words of realistic README prose, keeping every existing signal (installation, usage, features, tech stack, badges, demo link).

**Test plan:** `pytest tests/unit/test_readme_scorer.py -v` should go from `1 failed, 22 passed` (with `--runxfail`) to `23 passed`, with no `assert 51 > 100`.

**Unknowns:** I expect `overall_score > 0.7` to still hold, since the score was 0.87 at 51 words, but I will confirm by running it. I know a classmate has linked #95; per the class house rules I am posting my own plan from my own reproduction.

---

## Your branch

**Branch**

fix/63-readme-fixture-word-count

**Evidence**

Environment for both runs: Windows 11 Pro, Python 3.14.6, pytest 9.1.1, venv installed with `pip install -e ".[dev]"`.

Before (my Unit 2 reproduction, commit f89c06f, posted on issue #63):

```
> .\.venv\Scripts\pytest tests/unit/test_readme_scorer.py -v --runxfail
>       assert data["word_count"] > 100
E       assert 51 > 100
tests\unit\test_readme_scorer.py:60: AssertionError
readme_scored  category=minimal score=0.8717142857142858 word_count=51
FAILED tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals - assert 51 > 100
1 failed, 22 passed in 0.83s
```

Without `--runxfail` the same file gave `22 passed, 1 xfailed in 1.90s`.

After (branch fix/63-readme-fixture-word-count, commit 81193a8):

```
> .\.venv\Scripts\pytest tests/unit/test_readme_scorer.py -v
============================= test session starts =============================
platform win32 -- Python 3.14.6, pytest-9.1.1, pluggy-1.6.0 -- C:\dev\projects\CodePath\AI301\pathreview-ai301-fa26-s1\.venv\Scripts\python.exe
collecting ... collected 23 items

tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED [  4%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_no_content PASSED [  8%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_only_title PASSED [ 13%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_minimal PASSED [ 17%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_adequate PASSED [ 21%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_word_count_category_comprehensive PASSED [ 26%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_installation_section_detection PASSED [ 30%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_usage_section_detection PASSED [ 34%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_setup_keyword_counts_as_installation PASSED [ 39%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_quickstart_counts_as_usage PASSED [ 43%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_badge_detection PASSED [ 47%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_demo_link_detection PASSED [ 52%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_tech_stack_section_detection PASSED [ 56%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_technologies_keyword_counts PASSED [ 60%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_overall_score_calculation PASSED [ 65%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_missing_readme_content_key PASSED [ 69%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_result_has_all_required_fields PASSED [ 73%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_case_insensitive_section_detection PASSED [ 78%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_whitespace_only_readme PASSED [ 82%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_example_keyword_counts_as_usage PASSED [ 86%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_score_scales_with_word_count PASSED [ 91%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_try_it_as_demo_indicator PASSED [ 95%]
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_built_with_counts_as_tech_stack PASSED [100%]

============================= 23 passed in 0.41s =============================
```

`test_readme_with_all_quality_signals` now shows PASSED instead of XFAIL, and `assert 51 > 100` no longer appears. A separate check of the scorer on the new fixture gave a word count of 554, category `comprehensive`, and an overall_score of 1.0.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `python run_eval.py --rubric ... --evidence ... --limit 3` (partial smoke run): "agreement: 3/3 scored items".
2. `python run_eval.py --rubric ... --evidence ... --save-run eval-run.txt` (full run): "agreement: 18/20 scored items  (bar: 18/20: PASS)". The two misses were pkg-05 and pkg-14.

I did not revise any file between these two runs. The last score, 18/20, matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

pkg-05 (category clear-accept). My rubric decided reject; the gold label is accept. The harness row reads:

```
pkg-05  clear-accept       accept  reject   NO     failed: unknowns-honest
```

[PACKAGE ANALYSIS REASON: replace this line with the explanation of what in pkg-05's plan my unknowns-honest check read as false confidence or a hidden unknown, quoting the plan text.]

**Check rationale**

unknowns-honest, as it reads in my uploaded `rubric.md`:

"Pass if the plan does not claim more than the evidence shows, and states what it has not checked. Fail if it asserts certainty about code or effects the evidence never touched (a confirmed root cause with no evidence, "no side effects") or hides an obvious unknown."

It reads that way because the failure families in the rubric template include "the unknowns are dressed up as certainty", and I wanted a check that fails a plan which claims more than the repro evidence shows, while still passing a plan that lists what it has not checked. I wrote it with two sides on purpose: a plan is not penalized for admitting unknowns, only for asserting certainty beyond the evidence. I did not revise it after the full run, because the run recorded a fingerprint of each file and changing it would no longer match the `eval-run.txt` I uploaded.

**Trade-offs**

This check gives up clear-accept plans that sound confident. In my full run it failed both pkg-05 (note: "failed: unknowns-honest") and pkg-14 (note: "failed: executable, unknowns-honest"), and the gold label for both is accept. Those two misses are why my score is 18/20 and not higher, so I accept that this check can reject a plan that is fine.

Nothing else changed after the full run, and I know because I made no edits to `rubric.md`, `procedure.md` or the evidence guide after it, so the uploaded files match the fingerprints recorded in `eval-run.txt`. A second limit I noticed in live mode: my `procedure.md` only describes eval mode (it says "The package is the whole world" and reads a "repo-facts block"), so in live mode the skill had to fill in the sources itself.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
