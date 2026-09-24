# SHOTLIST — w1-softmax-offset

All beats: `shot.type REMOTION`, `source own`, pattern `SoftmaxOffset`
(`brutalist.art/runtime/remotion/src/scenes/SoftmaxOffset.tsx`; a copy is in
`remotion/` in this folder). No Manim, no LaTeX, no stills, no gen-AI, no pantry.
Each beat's clip is exactly as long as its measured narration.

| Beat | Mode | What moves | Label on screen |
|---|---|---|---|
| B01A | pipeline step 1 | SCORES box springs in | diagram |
| B01B | pipeline step 2 | → PROBABILITIES box springs in | diagram |
| B01C | pipeline step 3 | → PICK box; "that's the loop" caption | diagram |
| B01D | pipeline step 4 | PROBABILITIES box highlighted, others fade; question appears | diagram |
| B02A | table | logits 1, 2, 3 shown; probability column empty | recorded output |
| B02B | table | printed probabilities fade in beside the logits | recorded output |
| B02C | table | source credit line turns accent colour | recorded output |
| B03A | shift | **left column counts 1→1001, 2→1002, 3→1003; right column stays frozen, outlined**; sweep-check footnote | recorded output |
| B03B | compare | both runs' 17-digit values; highlight sweeps across every digit; `bitwise identical?  True` flashes | recorded output |
| B03C | cancel | fraction "its weight / total of all weights"; "× same factor" chips appear top and bottom, then are struck through | constructed diagram |
| B03D | intermediates | both inputs → "minus max" → `[-2, -1, 0]` | recorded output |
| B04A | rows | `[1000, 1000] → 0.500000, 0.500000` | recorded output |
| B04B | rows | `[0, 0]`, `[-5, -5]` rows appear on cue | recorded output |
| B04C | rows | first three dim; `[1, 2]` and `[1001, 1002]` appear highlighted as a pair | recorded output |
| B04D | rows | "A huge logit is not a confident model."; dark box: `naive exp at [1000, 1000]:` / `OverflowError: math range error` | recorded output |
| B05 | card | dark card, lines reveal: WHAT THIS DOES NOT SHOW → shown / not shown / 66.52% / nothing here says the model is right | — |
