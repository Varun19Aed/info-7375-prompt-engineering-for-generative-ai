# FRICTIONAL.md

Ashwin Thankachan — INFO 7375, Week 1 Explainer Video

The first two entries are my own notes. From the toolkit build (2026-09-23, ~21:50) onward,
Claude Code organised the entries from the session record (commands, printed output, file
timestamps) and my answers in chat. Understanding and decisions are mine, in my words.

---

## 2026-09-23 — Choosing the concept

- **Tried / expected:** expected to pick a topic quickly and build the same evening.
- **Happened:** couldn't pick; logits, softmax, temperature and seeds were just words to me. I also
  mixed up the 25-pt Week 1 video with the 100-pt Assignment 01 and looked for code points in
  the video rubric. There are none (15 explanation / 2.5 Frictional / 2.5 GitHub / 5 RQ).
- **Did:** worked the mechanism bottom-up (scores → percentages → weighted draw). Chose the
  shared-offset concept because I could explain it completely.
- **Claude:** explained the two assignments apart, ran the softmax comparisons, proposed the beat
  structure and the Beat 5 boundary. Accepted.
- **Understand / don't:** thought the offset disappears *because softmax subtracts the max*
  (corrected below). Still don't know why exponential is the right transform rather than just
  dividing raw scores by their total.

## 2026-09-23 — Prerequisite check

- **Happened:** `Python 3.9.6` (below the 3.11 minimum; it's the macOS system Python) and
  `zsh: command not found: ffmpeg`. git 2.51.0, node v25.8.0, npm 11.11.0 OK.
- **Planned:** Homebrew `python@3.12` + `ffmpeg`, leaving the system Python alone.
- **Claude:** identified 3.9.6 as the system Python.

> *Correction (2026-09-24):* those installs were planned, not done. At ~21:50 `python3.12` and
> `ffmpeg` were still "not found". See the next entry.

## 2026-09-23 (~21:50–22:05) — Toolkit install

- **Expected:** toolkit, evidence folder, Python 3.12 and ffmpeg already in place, as my build brief said.
- **Happened:** none existed. The toolkit's own doctor stopped on "ElevenLabs reference found" and
  its smoke test failed with `metadata.slug must be a filename, not a path` (fixture slug
  `_smoke`), both upstream bugs.
- **Did:** approved one global install, `brew install ffmpeg` (9.0.2). Used the existing Python
  3.13.7 (`kokoro-onnx` needs <3.14); everything else stayed local in `brutalist.art/`.
- **Claude:** found and ran all of this. Honestly, for me this part was straightforward because
  Claude did the installs; I didn't hit the problems myself.
- **Evidence:** toolkit commit `6a8380ae169cca81e0633664a65c958f5c12ab4b`.

## 2026-09-23 (21:58) — Evidence files

- **Happened:** `reference-output.txt` and `offset-output.txt` matched my brief digit for digit
  (`0.09003057317038046, 0.24472847105479764, 0.6652409557748218`, `bitwise identical?  True`),
  and were byte-identical under Python 3.9.6.
- **Claude:** generated all three files and added `intermediates_evidence.py`: both inputs become
  `[-2, -1, 0]` after subtracting the max, and all 1001 offsets 0..1000 are bitwise identical,
  covering every frame of the Beat 3 count-up. Accepted.
- **Not yet done:** I haven't re-run these myself (as of 2026-09-24 morning).

## 2026-09-23 — Script defensibility

- **Happened:** Claude flagged that Beat 3 credited the cancellation to max-subtraction (the same
  thing I wrote above), and that Beat 1 said "percentages that add up to one".
- **Did:** accepted a rewritten Beat 3 (same factor top and bottom → cancels; max-subtraction →
  the exact same digits) and "probabilities" in Beat 1.
- **Understand now:** if we add 1000, the size of the scores doesn't matter, because it cancels
  out in the numerator and the denominator.
- **Evidence:** `FACTCHECK.md` rows B03C, B03D.

## 2026-09-23 (22:05–22:23) — Audio and draft 1

- **Happened:** narration measured 137.06 s (2:17), under my 2:45 target. Draft 1 compiled (16/16
  beats) but Gate V failed: 3 MAJOR "underfill", B01A 49% and B05 26%/35% of the safe area (min 55%).
- **Claude:** wrote the `SoftmaxOffset` component and build/sync/verify tools (110/110 on-screen
  numbers traced); fixed a 15 s cutoff that hid Beat 5's last line.
- **Evidence:** `_qc/REPORT.md`; commit `7d8b432`.

## 2026-09-24 — Watching draft 1 (revision)

- **Expected:** a finished explainer.
- **Happened:** I followed that it's about logits and how the next token is predicted, but had
  no clue what softmax actually is or what the whole video was for. The start and the end felt abrupt.
- **Did:** asked Claude to explain softmax from scratch; it walked through e^score → add up →
  divide, with a slider demo where adding 1000 didn't move the bars. Asked for three changes:
  name and define softmax in Beat 1, add an intro that asks the question, and add a closing recap.
  These make the video longer, but for a reason a viewer gave, not padding.
- **Evidence:** next commit (revision). Folder decided: `fall-2026/ashwin-t/week-01-video/`.
  Still open: fork vs. direct push.
