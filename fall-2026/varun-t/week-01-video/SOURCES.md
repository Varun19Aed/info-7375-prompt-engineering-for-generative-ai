# Sources and Attribution

## Course Material

### INFO 7375 — Chapter 1: Randomness and First Prompts

The primary technical source for this video is the Chapter 1 INFO 7375 lesson material and its accompanying reference implementation:

```text
lessons/01-randomness-and-first-prompts/code/main.py
The lesson implementation was used to reproduce the softmax probabilities for the constructed input `[1, 2, 3]`.

Locally reproduced probabilities:

[0.09003057317038046, 0.24472847105479764, 0.6652409557748218]

The lesson's maximum-subtraction implementation also motivated the video's explanation of numerical stability.

## Constructed Examples

The video uses `[1, 2, 3]` as a constructed lesson input. These scores are not presented as the output of a real language model.

The video also uses `[1000, 1000]` as a constructed numerical-stability example.

In the local Python environment, evaluating `math.exp(1000)` directly produced:

OverflowError: math range error

After subtracting the maximum, `[1000, 1000]` becomes `[0, 0]`, producing exponential weights `[1.0, 1.0]` and probabilities `[0.5, 0.5]`.

## Brutalist Video Toolkit

The video was built using the Brutalist video toolkit created by Nik Bear Brown:

https://github.com/nikbearbrown/brutalist.art

Brutalist provided the video-building workflow, Remotion scene infrastructure, quality-control tooling, and visual conventions used during production.

## Production Tools

- Kokoro — local narration generation.
- Remotion — programmatic video scenes and animation.
- Matplotlib — mathematical expressions rendered as SVG for the algebra scene.
- FFmpeg — video and audio assembly and final rendering.
- Python — numerical reproduction, build scripts, and supporting tooling.

No paid media-generation API was used for the final video.

## AI Assistance

### Claude Code

Claude Code was used during the initial Brutalist workflow for planning, scaffolding the reel, creating and editing beat-sheet content, generating initial scene implementations, and assisting with build/debugging tasks.

### ChatGPT

ChatGPT was used for selecting and narrowing the Chapter 1 concept, explaining and checking the softmax mechanism, planning the storyboard, reviewing narration and scene content, troubleshooting the Brutalist workflow, assisting with custom Remotion scenes, interpreting quality-control reports, reviewing visual output, and preparing submission documentation.

All commands were executed locally by Varun Tadimeti. Numerical outputs used as evidence were reproduced locally, and rendered video scenes were manually reviewed before the final export.

## Attribution Note

The `@NikBearBrown` branding appearing in portions of the video is part of the Brutalist template/toolkit conventions.

Student identification is provided separately in the video as:

INFO 7375 · Northeastern University
Varun Tadimeti · Week 1

## Limitations

The explanation demonstrates why a common shift leaves the mathematical softmax distribution unchanged and why subtracting the maximum avoids unnecessarily large positive exponentials.

It does not establish that the teaching implementation is immune to every possible extreme floating-point or numerical input.
