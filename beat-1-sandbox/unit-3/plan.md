# Plan for #63: README scorer test fixture is too short for its own word-count assertion

## Diagnosis

`test\_readme\_with\_all\_quality\_signals` in `tests/unit/test\_readme\_scorer.py` fails because its fixture README is too short for the test's own assertions, not because the scorer is wrong.

Repro evidence I rely on (from my Unit 2 reproduction comment, commit f89c06f, Windows 11 Pro, Python 3.14.6, pytest 9.1.1), command `.\\.venv\\Scripts\\pytest tests/unit/test\_readme\_scorer.py -v --runxfail`:

```
>       assert data\["word\_count"] > 100
E       assert 51 > 100
tests\\unit\\test\_readme\_scorer.py:60: AssertionError
readme\_scored  category=minimal score=0.8717142857142858 word\_count=51
1 failed, 22 passed in 0.83s
```

The scorer reports `category=minimal` for the 51-word fixture. Reading `agent/tools/readme\_scorer.py` lines 68-73, the scorer returns "minimal" under 100 words, "adequate" under 500 words, and "comprehensive" otherwise. The test also asserts `data\["word\_count\_category"] == "comprehensive"`, so the fixture needs at least 500 words, not just more than 100. My repro stopped at the first failing assertion (line 60), so I have not yet observed the category assertion fail. That requirement comes from reading the scorer, and I will confirm it by running the test.

## Scope

In scope: extend the README fixture string inside `test\_readme\_with\_all\_quality\_signals`, and remove that test's `@pytest.mark.xfail(strict=True, ...)` marker, because a strict xfail on a passing test would report a failure.

Not in scope: changing `agent/tools/readme\_scorer.py`, changing any assertion in the test, changing the scorer's thresholds, or touching any other test.

## Files I will touch

* `tests/unit/test\_readme\_scorer.py` only.

## Approach

1. In `test\_readme\_with\_all\_quality\_signals`, extend the `readme` fixture to about 550 words of realistic README prose, so the scorer counts at least 500 words (the scorer counts with `content.split()`, so every whitespace-separated token counts).
2. Keep every signal the test checks: the Installation, Usage, Features and Tech Stack sections, the two badge images, and the Live Demo link.
3. Remove the `xfail(strict=True, reason="issue #63 ...")` decorator from this test.
4. Leave all assertions unchanged.

## Test plan

Before the fix (from my Unit 2 repro): `.\\.venv\\Scripts\\pytest tests/unit/test\_readme\_scorer.py -v --runxfail` gives `1 failed, 22 passed` with `assert 51 > 100`.

After the fix: `.\\.venv\\Scripts\\pytest tests/unit/test\_readme\_scorer.py -v` should give `23 passed` with no xfail, and the output should no longer contain `assert 51 > 100`. I will also print the fixture's word count from the `readme\_scored` log line to confirm it is at least 500.

## Risks and unknowns

* Not yet observed: that the category assertion needs 500 words. I inferred it from reading the scorer, and the after-fix run will confirm or contradict it.
* `overall\_score > 0.7` should still hold, since the score was 0.87 with 51 words and the word-count bonus can only rise with more words, but I have not verified the scoring weights, so I will confirm it by running the test.
* I have not run the rest of the unit suite. I only expect the file's other 22 tests to be unaffected, because only this one test's fixture changes.
* A classmate has linked PR #95 to this issue. I am building my own change from my own reproduction.

## Deviations

No deviations from the plan. I changed only tests/unit/test\_readme\_scorer.py: the fixture is now 554 words, which the scorer counts as "comprehensive", and I removed the xfail marker. The unknowns I listed resolved as expected: the category assertion did need 500+ words, and overall\_score is 1.0, above 0.7. I ran only the test file, not the full unit suite.

