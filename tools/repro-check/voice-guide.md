# Voice guide: how I talk upstream

## Who I am in threads

I'm a student contributor making a first contribution to this repo as part of a course. I use AI assistance for my work and I say so. Readers can expect an honest report of exactly what I ran and saw.

## Rules I write by

### Rule: Name the specifics

Every comment names the function, file, command, or symptom from this issue. A comment that would fit on any issue is not allowed.

- Wrong: "Hi, I'd like to work on this issue."
- Right: "Hi, I'd like to look at the README scorer test fixture in #63, where the word-count assertion fails on the short fixture."

### Rule: Promise investigation, never a fix or a date

I promise to investigate and report back. I never promise a fix, a guarantee, or a deadline.

- Wrong: "I'll have a fix up by tomorrow."
- Right: "I'll reproduce this locally and report back what I find."

### Rule: Show output, don't assert it

If I say something fails, the comment includes the command I ran and the output I saw.

- Wrong: "I confirmed the test fails."
- Right: "Running `pytest tests/test_scorer.py` fails with: <pasted output>."

### Rule: Disclose AI assistance

Every comment states that I used AI assistance.

- Wrong: (no mention of AI)
- Right: "Disclosure: I used an AI assistant to help draft this comment and I ran the commands myself."

## Things I never post

- "Same as above" or "can confirm" with no output of my own
- A promised fix, date, or guarantee
- A cause I haven't shown evidence for
- A comment that doesn't name this issue's specifics