# Softmax, Shifted

**Student:** Varun Tadimeti  
**Course:** INFO 7375  
**Assignment:** Week 1 Video  
**Runtime:** 2:53  
**Concept:** Numerical stability in softmax

## Overview

This video explains why subtracting the maximum score before computing softmax changes the intermediate numerical values but does not change the mathematical probability distribution.

Subtracting the same constant from every score introduces the same multiplicative factor into every exponential term. Because that factor appears in both the numerator and denominator, it cancels during normalization.

## Worked Example

The video uses the constructed lesson input:

`[1, 2, 3]`

At temperature T = 1, subtracting the maximum value 3 gives:

`[-2, -1, 0]`

The shifted exponential weights are approximately:

`[0.135335, 0.367879, 1.0]`

After normalization, the probabilities are:

`[0.0900305732, 0.2447284711, 0.6652409558]`

These values were reproduced locally using the Chapter 1 reference implementation.

The video also uses the constructed example `[1000, 1000]`. In the local Python environment, `math.exp(1000)` produced an `OverflowError`. Subtracting the maximum changes the scores to `[0, 0]`, producing weights `[1, 1]` and probabilities `[0.5, 0.5]`.

## Mechanism

For a common shift c at temperature T = 1:

`exp(x_i - c) = exp(x_i) * exp(-c)`

The factor `exp(-c)` appears in both the numerator and denominator of softmax and therefore cancels. More generally, at temperature T, the common factor is `exp(-c/T)`.

## Limitation

Maximum subtraction avoids unnecessarily large positive exponentials, but this demonstration does not establish that the implementation handles every possible extreme numerical input. Floating-point and implementation limits still exist.

## Reproducibility

The primary numerical example comes from the INFO 7375 Chapter 1 reference implementation:

`lessons/01-randomness-and-first-prompts/code/main.py`

Locally reproduced output for `[1, 2, 3]`:

`logits: [1, 2, 3]`

`peak: 3`

`shifted: [-2, -1, 0]`

`shifted weights: [0.1353352832366127, 0.36787944117144233, 1.0]`

`probabilities: [0.09003057317038046, 0.24472847105479764, 0.6652409557748218]`

## Production

The video was produced with the Brutalist video toolkit using:

- Kokoro for local narration
- Remotion for visuals and animation
- Matplotlib-generated SVG for mathematical expressions
- FFmpeg for video/audio assembly
- Python for numerical reproduction and supporting build tasks

AI assistance and source attribution are documented in `SOURCES.md` and `PROMPTS.md`.

## Deliverables

The submission includes:

- `README.md`
- `softmax-shifted.mp4`
- `beat_sheet.json`
- `BUILD-PROMPT.md`
- `SOURCES.md`
- `FRICTIONAL.md`

## Why I Chose This Concept

I chose this concept because subtracting the maximum in softmax initially looks like it should change the result, but the algebra shows why the probability distribution remains unchanged while making the computation numerically safer.

## How to Rebuild

From the root of the Brutalist repository, run:

`./art final books/info-7375/youtube/softmax-shifted/`

The build uses the local Brutalist environment with Kokoro, Remotion, FFmpeg, and Python. The detailed prompts, setup steps, and commands used during the build are documented in `BUILD-PROMPT.md`.
