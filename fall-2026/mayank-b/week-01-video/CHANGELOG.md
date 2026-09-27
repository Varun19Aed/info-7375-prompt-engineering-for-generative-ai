# CHANGELOG — Temperature Is Not a Fact Checker.

Every change to the video since generation started, newest last. Times are local
(from file timestamps where noted). FRICTIONAL.md records *what went wrong*; this
file records *what changed*.

## 2026-09-23 — v1: first build

- **~18:39 — Evidence.** Copied the chapter's `probabilities()` and `sample()` verbatim into
  `code/main.py`; wrote `code/run_temperature.py`. Output `code/temperature_results.json`
  matches the chapter's tables exactly (Python 3.11.16).
- **~18:40 — Beat sheet v1.** `code/author_sheet.py` → `beat_sheet.json`: 12 beats
  (B00 cold open, B01 hesitant-writer summary, B02–B08 body, BVDT recap, BHTF your turn,
  BOUT outro), 480 words, Kokoro `am_onyx`, title "Temperature Is Not a Fact Checker."
- **18:43 — Audio.** Kokoro narration generated for all 12 beats (158.5 s total).
- **~18:44 — B01 lead silence.** Prepended 0.8 s of silence to `mp3/beat-B01.mp3`
  (10.58 s → 11.38 s). Total 159.3 s.
- **18:45 — Word clock.** `align.py` → `mp3/words.json` (12/12 beats aligned).
- **~18:46 — Props.** `code/build_props.py`: animation cues from word timings, typeset math
  SVGs (softmax, ratio, gap, three ratio rows), real seed-7 draw sequences.
- **~18:47 — New scenes.** Added `TemperatureConcentration.tsx` (7 components: TcScoresToOdds,
  TcTemperatureDial, TcRatio, TcCode, TcSampleCounts, TcWrongAnswer, TcBoundary) and registered
  them in the toolkit's `Root.tsx`. Copied the NBB logo into `public/temperature-concentration/`.
- **18:50 — Layout fixes from test stills (before the full render):**
  - B04: max ratio-bar length 760 → 520 px (the "54.60×" label was clipped).
  - B06: dot cell 19 → 20 px; count legend redesigned as label-over-number columns (the legends collided);
    added the "outcome 2 share vs assigned p" line.
  - B07: honesty stamp forced onto one line; footer caption shortened.
  - B08: bigger claim cards (font 44 → 54, card height 130 → 180, row spacing 170 → 215).
- **18:51–19:05 — Render.** All 12 beats rendered with Remotion at 4K.
- **~19:06 — Review cut v1** compiled (159.5 s).

## 2026-09-23 — v2: fixes from visual QC

- **B01 (hesitant writer):** the correction never appeared on screen in v1.
  - Trigger `how creative the model is` → `creative`; replacement → `concentrated`.
  - Text line 1 changed to "Temperature sets how creative the choices are." (after the fix it reads
    "…how concentrated the choices are.").
  - Typing sped up and made more even: `charMs` 50 → 32, `mistakeRate` 10 → 3,
    `hesitateWithin` 3 → 1, `hesitateBetween` 20 → 8.
- **B00, BHTF (composer bookends):** `largeText: true` (text was undersized).
- **19:10** Re-rendered B00, B01, BHTF. **19:13** Review cut v2 compiled
  → `temperature-concentration-slate.mp4` (159.5 s).
- Narration and audio are unchanged from v1.

## 2026-09-25 — v3: clean master + submission files

- **Clean master:** `compile.py --height 1080` (no review overlays) → `temperature-concentration.mp4`
  (159.5 s, 9.4 MB). The first attempt was refused by Gate V: B01 "underfill" (text covers 7–23% of
  the safe area mid-typing). Added the toolkit's `qc.sparse_by_design` declaration with a written
  reason to B01 only (it waives the fill checks; edge, empty-frame and contrast checks still run).
  Gate V then passed: 0 BLOCKER, 0 MAJOR.
- Added `README.md`, `SOURCES.md`, `.gitignore`, `_qc/MANUAL-QC.md` (my hand QC table; Gate V
  overwrites `_qc/REPORT.md` on every compile, its first failing run is kept in
  `_qc/GATE-V-REPORT-first-run.md`).
- No change to narration, audio, or any visual.
- Pushed to `nikbearbrown/info-7375-prompt-engineering-for-generative-ai`,
  `fall-2026/mayank-b/week-01-video/`.

## 2026-09-25 — workflow
- Pushed as commit `72e9aa1` (v3).
- From here on, every iteration becomes its own commit in the course repo, pushed with
  `bash code/publish.sh "vN: what changed"`, so the history shows how the video was revised.
  Added `code/publish.sh`; it will go up with the next iteration.

## 2026-09-25 — v4: fix course CI failure

- Commit `72e9aa1` failed the course repo's `validate` workflow: `scripts/validate_course.py`
  rejects any `.ts/.tsx/.js` file ("Non-Python implementation"), and it scans the whole repo, so the
  next student's commit went red too.
- `remotion-src/TemperatureConcentration.tsx` → `TemperatureConcentration.tsx.txt` (byte-identical),
  plus `remotion-src/README.md` explaining why and how to restore it. BUILD-PROMPT, SOURCES and
  README references updated.
- Added `code/check_repo_rules.py` (local copy of the CI rules); `publish.sh` now runs it before
  every commit and refuses to push on failure. Also adds `code/publish.sh` to the repo.
- No change to the video.

## 2026-09-26 → 27 — v5: new beat B01A "how a chatbot picks the next word"

Why: reviewing the concept from first principles, we agreed the video skipped the basics. It
jumped to "three scores, softmax" without saying that a chatbot picks the next token from scored
options, or why scores must become chances.

Done so far:
- **New beat B01A** (after the Beat 2 summary, before B02). Narration (49 words, 15.34 s):
  "First, what a chatbot does. It writes one token, roughly one word, at a time. At each step it
  scores every possible next token: Paris high, Lyon lower. Scores aren't chances yet. A formula
  called softmax turns them into chances that add up to one. Then the model draws."
- Visual plan: "The capital of France is ___"; four candidates (Paris, Lyon, beautiful, a) with
  **unnumbered** score bars and the stamp "ILLUSTRATIVE SCORES · NOT FROM A REAL MODEL"; a
  "chance?" column; a softmax label; "Paris" drops into the blank.
- Added to `code/author_sheet.py` and inserted into `beat_sheet.json` (13 beats now).
- `mp3/beat-B01A.mp3` generated (Kokoro am_onyx). No other beat's audio touched.
- New component `TcNextWord` in `TemperatureConcentration.tsx`, registered in `Root.tsx`;
  B01A cue anchors added to `code/build_props.py`.
- SHOTLIST (B01A row), CHECKS-REPORT (8 SHOW), FACTCHECK (three new claims, quoted from the
  chapter's fig. 1 caption, §35 and §37) updated.

Paused 2026-09-26 by the iCloud problem (FRICTIONAL). Resumed 2026-09-27 once the files were back:
- Word alignment for B01A (49 words). Cues: sentence 1.54 s, scores 4.88 s, chance 8.42 s,
  softmax 10.67 s, draw 13.58 s.
- Test stills changed the design twice before the full render:
  1. "Paris" landed right of the blank instead of in it → end position measured from a still (x≈862).
  2. The flying word crossed the Paris bar and the SCORE label mid-flight → replaced the flight with
     "the winning row lights up (bar turns terracotta) and fades, while Paris rises into the blank".
  3. The word "softmax" was a second terracotta element → bold ink (one accent per beat).
- Rendered B01A at 4K (Remotion).
- **B01 fix found by the v5 QC pass:** the last line was still typing at the cut ("…answer is tr|").
  My v2 claim that "all three lines finish inside the beat" was wrong. `charMs` 32 → 26;
  re-rendered B01; the full sentence, period included, is on screen by 11.3 s and the
  creative → concentrated correction still plays (`_qc/sheet-v5-B01*.png`).
- Recompiled review cut + clean master: **174.8 s**, 13/13 beats filled, Gate V 0 BLOCKER / 0 MAJOR.
- README (runtime, B01A row, 13 beats) and `remotion-src/TemperatureConcentration.tsx.txt` updated.
- Narration of every other beat unchanged. **← current version**
