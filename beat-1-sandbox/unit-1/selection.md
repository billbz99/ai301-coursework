# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63

**Verdict output**

All three issues pass every required check, so all three are accepted. I couldn't rank them by fit: the "Your fit profile" section in `scope.md` is still the placeholder text, and fit is the only thing the skill uses to order accepted issues. They also tie on the two preferred checks, so the list below is in the order you gave them.

`gh` isn't installed on this machine, so I gathered the evidence from the public GitHub REST API instead. Dates are measured against today, 2026-10-04.

**Accepted (no fit ranking):**
1. **#63 – README scorer fixture too short.** You'd lengthen a test fixture or fix its assertion. You only need pytest to check it.
2. **#64 – Relevance scorer "partial overlap" fixture.** Same kind of fixture fix. You only need pytest.
3. **#61 – Health check `SELECT 1` needs `text()`.** A one-line fix in `api/routes/health.py`. To check it you need Docker and Postgres running. One comment notes that `/health` still won't return 200 until #62 is fixed (open PRs #76 and #86 cover #62).

If you want the setup work to break the tie, #63 and #64 are lighter than #61. That's my observation, not a rubric result. Fill in your fit profile and I'll rank them properly.

**Rejected:** none.

Things worth knowing before you pick:
- **Claim comments:** every issue has several classmates' claim comments: 3 people on #63, 5 on #64, 8 on #61. The Path Review house rule says to ignore these, so `unclaimed` passes on assignees and PRs alone.
- **PR checklist:** the target tests in #63 and #64 are marked `xfail(strict=True)`. The PR template requires you to remove that marker in your fix.
- **Maintainer response:** `maintainer-responsive` passes as the rubric is written. The only two maintainer comments in the repo (Aburke225 on #43 and #52, 2026-09-16) came within 14 days. But no maintainer has replied in any of these three threads. You might add "replied to contributor comments" to the rubric.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Newest commit 2026-09-16 by human Aburke225 (Andrew Burke), 18 days ago; all 5 recent commits human"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (no releases), within 180 days"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no linked or mentioned PRs; classmate claim comments (AliceKindle2, riyag0, Stephen-Agyemang) ignored per Path Review house rule"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "\"Extend the fixture (or correct the assertion) so the test validates what it intends to\" - single test fix with repro"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template say nothing about AI"},
      {"name": "good-first-label", "grade": "pass", "evidence": "labels: bug, good first issue, tests, tier-1"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled collaborator replies (Aburke225 on #43, #52, 2026-09-16) within 14 days of issues opened 2026-09-10"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Newest commit 2026-09-16 by human Aburke225 (Andrew Burke), 18 days ago; all 5 recent commits human"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (no releases), within 180 days"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; only cross-ref is Cael-Pairrett/CodePath-Repo PR #1 (closed, a course write-up in a personal repo, not a fix here); claim comments ignored per house rule"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "\"Fix the fixture so the overlap is genuinely partial\" - single test-fixture fix with repro"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template say nothing about AI"},
      {"name": "good-first-label", "grade": "pass", "evidence": "labels: bug, good first issue, tests, tier-1"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled collaborator replies (Aburke225 on #43, #52, 2026-09-16) within 14 days of issues opened 2026-09-10"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/61",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Newest commit 2026-09-16 by human Aburke225 (Andrew Burke), 18 days ago; all 5 recent commits human"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (no releases), within 180 days"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; cross-refs are issues #62, #26 and a bot issue, not PRs; open PRs #76/#86 fix #62, not #61; claim comments ignored per house rule"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Wrap \"SELECT 1\" in sqlalchemy.text() in api/routes/health.py - one call site, confirmed by a commenter's repo-wide grep"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template say nothing about AI"},
      {"name": "good-first-label", "grade": "pass", "evidence": "labels: bug, good first issue, api, tier-1"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled collaborator replies (Aburke225 on #43, #52, 2026-09-16) within 14 days of issues opened 2026-09-10"}
    ],
    "verdict": "accept"
  }
]
```


**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Partial run (--limit 3), before the Windows fix: 1/1 scored items, 2 items errored.
2. Same partial run after setting PYTHONUTF8=1: 3/3.
3. Full run: 18/20.

**Issue analysis**

issue-19: my rubric said reject, the gold label is accept. The failing check was scope-bounded. The issue body says "There are two potential causes which should be fixed:" and then lists "Additional suggestions", so my check read it as an umbrella issue with a list of sub-items. It was opened by a COLLABORATOR with no assignee, no linked PRs and no comments, so none of my other checks objected.

**Check rationale**

scope-bounded: "Pass if the issue asks for one bounded piece of work. Fail if ANY is true: it is an umbrella or tracking issue (a list of sub-items to split into separate work); a maintainer says the fix needs changes to core internals; the thread shows the design is still being debated with no maintainer decision; or it is a usage or support question rather than a change request. A short body, an acceptance-criteria checklist, or a bug report without reproduction steps is NOT a fail."

I wrote it from the evidence guide's scope section, which says to grade the size of the work and not how polished the writeup is. That's why the last sentence is there.

**Trade-offs**

This check gives up issues like issue-19, where a list in the body is suggestions and not separate tasks. That cost me one disagreement. I did not change the rubric after the full run so that rubric.md still matches eval-run.txt.

---

## Selection rationale

1. Fit and time: #63 is a small test-fixture fix. I only need pytest, no Docker or database, so it fits the time I have.
2. The verdict confirmed the issue is one bounded task, unassigned, with no linked PRs, in an active repo. It could not judge setup effort, and it could not see that no maintainer has replied in this thread.
3. Difficulty claiming it: three classmates have already commented on it. The house rule says to claim anyway, so I will, but I expect to overlap with others.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
