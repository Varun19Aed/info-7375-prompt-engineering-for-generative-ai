# 665.24 Is Not a Promise

**Riya Kapadnis** · INFO 7375, Week 1 Explainer Video · kapadnis.ri@northeastern.edu

**Concept (one, from Chapter 1 Part 2):** expected count (665.24) versus observed
count (630) — an expected count is a rate times a number of draws, not a forecast
that any single run will produce it.

**Why this one:** the lesson's own sampler predicts token 2 will appear 665.24 times
in 1000 draws and then prints 630, and that 35-count gap is the smallest place in
Chapter 1 where you can watch the difference between a number a formula produces and
a number an experiment produces.

**Runtime:** 3:33.7 (213.66s) — measured from the rendered file with `ffprobe`, not estimated.
**Video:** `riya-k-expected-is-not-a-promise.mp4` — 1920×1080, 30 fps, H.264/AAC, 8.2 MB.
**Submitted via Canvas; not in this folder.** The repository's root `.gitignore` (line 33,
`*.[mM][pP]4`) excludes generated media at any depth, and
`prerequisites/github-submission.md` states that a video is not required for the GitHub
posting. Everything needed to rebuild the file bit-for-bit is here — see "Rebuild from
this folder" below.
**Cost:** $0.00. Kokoro narration and Manim rendering are local. No API keys, no paid
generation, no account, no upload.

---

## The seven beats

| # | Beat | What carries it |
|---|---|---|
| B00 | Title — name, course, and the question | The setup stated in three lines, closing on "what does an expected count actually claim?" |
| B01 | The lesson predicts 665.24 and prints 630 | Verbatim `main.py` output, then the −35.24 gap |
| B02 | Two different kinds of number | `0.6652409557748218 × 1000` written out; you cannot draw a fraction of a token |
| B03 | How big is a normal miss? | `sd = sqrt(n·p·(1−p))` = 14.92; 630 placed outside the ±2 SD band, z = −2.36 |
| B04 | Don't trust the formula — measure it | Histogram of 10,000 seeds builds; measured mean 665.234 lands on the predicted 665.24 |
| B05 | Where seed 7 actually falls | 89 of 10,000 seeds at or below 630 → the 0.89th percentile, below p1 = 631 |
| B06 | **What this does not establish** | A sampler biased to p=0.63 produces 630 **15.5× more readily** than the fair one |
| B07 | Conclusion | Not a bug · the sampler is fair · seed 7 is unusual — then the closing claim |

## What the video does not establish

Stated on screen in B06 and spoken in the narration: the reel shows that 630 is
*consistent with* a fair sampler. It does **not** show that a fair sampler is the only
thing that could have produced it. `P(630 | p=0.6652) = 0.001681` against
`P(630 | p=0.6300) = 0.026123` — both stories explain the observation, and one run of
1000 draws does not separate them.

## Numbers and provenance

Every figure spoken or displayed was computed on this machine by the scripts in this
folder. Nothing is illustrative and **no constructed distributions appear**, so no
frame needed a "constructed" label. The chapter text (`docs/en.md`) contains none of
these values — it has one line on the mechanism — so the citation is the run, not the
prose.

| File | What it is |
|---|---|
| `evidence/expected_vs_observed.py` | The analysis, with its saved run in `expected_vs_observed_output.txt` |
| `evidence/build_data.py` | Recomputes every on-screen figure into `video_data.json` |
| `video_data.json` | The single source the scenes read — no number is typed into `scenes.py` |
| `evidence/shift_invariance.py` | Superseded work on a different concept, kept because FRICTIONAL.md refers to it |

Determinism: the 10,000-seed sweep uses seeds 0–9999 with `random.Random(seed)`, so
re-running reproduces every figure exactly.

## Rebuild from this folder

Requires Python 3.11 (Manim 0.18 does not support 3.13), FFmpeg, `pkg-config`.

```bash
# 1. recompute every figure from the chapter's own code
python3 evidence/expected_vs_observed.py | tee evidence/expected_vs_observed_output.txt
python3 evidence/build_data.py                    # -> video_data.json

# 2. narration (Kokoro, local, free) -> audio/*.wav + audio/timings.json
python make_audio.py

# 3. the seven scenes at 1080p60
for S in B00_Title B01_TheGap B02_TwoKinds B03_HowBigIsANormalMiss B04_TenThousandSeeds \
         B05_WhereSeedSevenLands B06_WhatThisDoesNotEstablish B07_Conclusion; do
  python -m manim -qh --disable_caching --media_dir render -o "$S" scenes.py "$S"
done

# 4. sync each scene to its measured narration, then concatenate
python assemble.py                                # -> riya-k-expected-is-not-a-promise.mp4
```

`assemble.py` treats audio as the master clock: each scene is padded (last frame held)
or trimmed to its measured narration length. See `BUILD-PROMPT.md` for the full command
log and the environment versions.

## Contents

```
README.md              this file
FRICTIONAL.md          dated log, including the concept I abandoned and why
BUILD-PROMPT.md        prompts + commands that rebuild the video
SOURCES.md             what I made, what Claude contributed, third-party licences
beat_sheet.json        narration and visual plan (validates against Brutalist's schema)
scenes.py              seven Manim scenes; reads video_data.json
make_audio.py          Kokoro narration + duration measurement
assemble.py            audio-led sync and concatenation
video_data.json        computed figures the scenes read
qc-sheet.png           contact sheet used for visual QC
evidence/              analysis scripts and their saved output
audio/                 narration wavs + timings.json
riya-k-expected-is-not-a-promise.mp4
```
