# Week 1 Explainer Video — [1000, 1000] → [0.5, 0.5]

**Ashwin Thankachan** · INFO 7375 Prompt Engineering for Generative AI · Northeastern · Fall 2026

**Concept:** "[1000, 1000] → [0.5, 0.5], and what the shared offset never carried"
(Chapter 1, Part 2). Softmax only sees the *gaps* between logits; a shared offset
is discarded, so you can't read confidence from how large a logit is.

**Why this one:** it's the smallest idea in the chapter that can be explained
completely in a few minutes, and it corrects a real misconception: that a big
score means a confident model.

**Runtime:** 2:38 (158.5 s) · 16:9 · narration is a synthetic Kokoro voice (`af_bella`)

**Video:** `w1-softmax-offset.mp4`

**GitHub location:** `fall-2026/ashwin-t/week-01-video/`. The course docs say
`fall-2025/`, but this section is Fall 2026 and the repo's term folder is
`fall-2026/` (confirmed by me, 2026-09-24).

## What's in this folder

| File | What it is |
|---|---|
| `w1-softmax-offset.mp4` | the rendered video |
| `beat_sheet.json` | the reviewed narration + visual plan (18 beats, measured durations) |
| `BUILD-PROMPT.md` | the prompts and exact commands that rebuild it |
| `SOURCES.md` | what I made, what Claude contributed, tools, licences |
| `FRICTIONAL.md` | dated log |
| `FACTCHECK.md` | every claim → its evidence |
| `SHOTLIST.md`, `PROMPTS.md` | toolkit paperwork (Gate F) |
| `reference-output.txt`, `offset-output.txt`, `intermediates-output.txt` | the evidence: every on-screen number comes from these |
| `offset_evidence.py`, `intermediates_evidence.py` | scripts that print the evidence |
| `tools/` | beat-sheet builder, audio-cue sync, number verifier |
| `remotion/` | the custom Remotion component + the patch that registers it (compiles inside the Brutalist toolkit; editors show type errors here because React/Remotion are not installed in this repo) |

## Rebuild

Full steps in `BUILD-PROMPT.md`. Short version, from the parent folder that
holds `brutalist.art/`, the course repo, `w1-evidence/` and `w1-video/`:

```bash
source brutalist.art/.venv/bin/activate
python3.13 w1-video/tools/build_beat_sheet.py
python brutalist.art/runtime/scripts/generate_audio_kokoro.py w1-video
python3.13 w1-video/tools/sync_cues.py
python3.13 w1-video/tools/verify_numbers.py
(cd brutalist.art && ./art run ../w1-video --height 1080)
(cd brutalist.art && ./art final ../w1-video --height 1080 --out ../w1-video/final)
```

## Verify the numbers yourself

```bash
python3 w1-video/tools/verify_numbers.py
```

It checks that every on-screen number appears in the evidence files, and lists
every spoken number for comparison.
