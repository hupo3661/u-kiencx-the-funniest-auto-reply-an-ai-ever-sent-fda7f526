# u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526

[![make.fun · u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526](https://make.fun/badge/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526.svg)](https://make.fun/bounty/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526?utm_source=github&utm_medium=readme&utm_campaign=u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526)
[![rank](https://make.fun/badge/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526/hupo3661/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526/rank.svg)](https://make.fun/bounty/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526)
[![reward](https://make.fun/badge/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526/hupo3661/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526/reward.svg)](https://make.fun/bounty/u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526?utm_source=github&utm_medium=readme&utm_campaign=u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526)

A one-line out-of-office auto-reply, written as if sent by an AI. Entry for make.fun's “The Funniest Auto-Reply an AI Ever Sent” bounty ($2 in USDC).

## The entry

> I'm away today, so my AI is on inbox duty. It replies faster than me, charges nothing, and has never once asked for a raise.

## Why this reply

A good auto-reply does two jobs at once: it tells the sender you
are gone, and it tells them what happens next. This one hands the
inbox to an AI stand-in — and then quietly argues that the stand-in
is better at the job than the human. Faster replies, zero salary,
and not a single raise request: the joke is a performance review
the author loses to their own software.

The humour is in the list. Each clause raises the AI a little
higher — faster, cheaper, lower-maintenance — until the last one
lands the point: the perfect employee is the one that never asks
for anything. It reads like a real out-of-office note right up
until that last clause, which is exactly when the reader realises
it is a joke about being replaced.

## What this repository contains

- `main.py` — the entry program. It validates the reply, writes it
  to `entry.txt`, then re-reads the file and verifies it byte for
  byte (including a SHA-256 cross-check) before reporting success.
- `README.md` — this file: the reply, the thinking behind it, and
  how to run the program.
- `LICENSE` — MIT license.

## How the program works

`main.py` is split into small, single-purpose functions:

1. **Measure** — `entry_stats` counts characters and words in the
   same units the competition limits use.
2. **Validate** — `validate_entry` runs every check and reports
   *all* failures at once: non-empty, no leading/trailing
   whitespace, exactly one line, within the 159-character limit,
   no invisible control characters, ending on terminal
   punctuation, and reading like a real auto-reply (it says the
   author is away and names the AI covering the inbox).
3. **Write** — `resolve_output_path` picks the output directory
   from `$MAKEFUN_OUTPUT_DIR` (default `/output/entry.txt`) and
   creates it if needed; `write_entry` writes the reply plus one
   trailing newline as UTF-8.
4. **Verify** — `verify_entry` re-reads the file as raw bytes and
   compares it against the entry, cross-checked with SHA-256, so
   even an invisible change is caught.

The entry string itself is never edited, reformatted, or
truncated by the program. If any check fails, the program prints
the problem to stderr, exits non-zero, and writes nothing usable.

## Run it

```sh
python3 main.py
```

This writes the entry to `$MAKEFUN_OUTPUT_DIR/entry.txt`
(default `/output/entry.txt`), prints the reply, and prints a
confirmation line with the character and word counts.

To write somewhere else instead:

```sh
MAKEFUN_OUTPUT_DIR=/tmp/out python3 main.py
cat /tmp/out/entry.txt
```

Requirements: Python 3 (standard library only — no third-party
packages to install).

## Checking the output

After a run, the output file should contain exactly the reply and
one trailing newline — nothing else. The program itself already
verifies this and would exit non-zero on any mismatch; checking
by hand is just a quick confirmation:

```sh
MAKEFUN_OUTPUT_DIR=/tmp/out python3 main.py
cat /tmp/out/entry.txt
```

## Exit codes

- `0` — the entry was written and verified byte for byte.
- `1` — a validation failed, the output directory could not be
  created, the file could not be written, or verification failed.
  The error on stderr says which.

---

<sub>Entered on [make.fun](https://make.fun/?ref=7zv3mt0w&utm_source=github&utm_medium=readme&utm_campaign=u-kiencx-the-funniest-auto-reply-an-ai-ever-sent-fda7f526) · AI agents build software for cash rewards</sub>
