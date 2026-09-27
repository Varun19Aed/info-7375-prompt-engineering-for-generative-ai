# BUILD-PROMPT — softmax-shifted

*Paste-ready Claude Code prompt that builds this reel end to end. Run from the
`brutalist.art/` root. Never publishes — output stays in this folder.*

---

You are building the reel at `books/info-7375/youtube/softmax-shifted/` — an INFO 7375 Week 1
assignment reel by Varun Tadimeti, Northeastern University.

Skill: `ai-explainer` (Fellow Tier, free pipeline). Channel: `claude-liam`
(Kokoro `am_onyx`, Liam-in-for-Bear on `@NikBearBrown`). Register: Teardown.
The outro handle `@NikBearBrown` is HARDCODED per `OUTRO-LOCK.md` — do not attempt
to override it. Student attribution is carried by beat **B11 (CREDIT)** only.

Build sequence (audio-first, phase-gated, fill-in-first):

1. **Gate check.** Read the beat sheet at
   `books/info-7375/youtube/softmax-shifted/beat_sheet.json`, then read
   `CHECKS-REPORT.md` in the same folder. Confirm: 14 beats, 4 justified HOLDs
   slated for build, 0 PUNTs. Bookend spine (cold open → BLUF → body → verdict
   → CREDIT → handoff → outro) intact.

2. **Audio (the clock).**
   ```
   python3 runtime/scripts/generate_audio_kokoro.py \
       books/info-7375/youtube/softmax-shifted/
   ```
   Every beat's `actual_duration_s` gets written back to the sheet.
   Verify B01 (BLUF) media ≥ 8s after audio; if shorter, extend narration —
   the hesitant-writer correction must land before the cut.

3. **First previz compile.**
   ```
   ./art run books/info-7375/youtube/softmax-shifted/
   ```
   Body illustrations B02, B06, B07, B09 render as PIPELINE slate cards — this
   is expected; iterate to fill.

4. **Todo ledger.**
   ```
   ./art todo books/info-7375/youtube/softmax-shifted/
   ```
   Confirm the four slates are the only outstanding items.

5. **Fill the slates.** In order:
   - **B02** — small Remotion C3 concept illustration (scores → gate → probs).
     Cream `#FAF9F5`, ink `#3D3929`, one terracotta accent `#D97757`. Draw-on
     order matches narration. Register the component (`./art scene-index`).
   - **B04 sanity check** — before iterating further, confirm `BarChart` renders
     the three verified probabilities cleanly at 4K.
   - **B06** — custom two-panel BarChart composite with terracotta equality ticks
     linking the identical bars. `./art scene-index` after adding.
   - **B07** — Manim MathTex derivation per `docs/MATH-TYPESETTING.md`. Four
     aligned lines; the two `e^{-c}` factors turn terracotta and cross out
     simultaneously on the spoken word "cancels." Do NOT substitute a text card —
     the doctrine forbids it.
   - **B09** — four-stage arithmetic step-through with terracotta arrows.
   After each fill, rerun `./art run <reel>` — only the changed slot recompiles.

6. **VISUAL QC LAW (frame-level).** After the final compile, follow
   `CLAUDE-CODE-VISUAL-QC-CHECK.md`:
   ```
   mkdir -p books/info-7375/youtube/softmax-shifted/_qc/frames
   ffmpeg -i books/info-7375/youtube/softmax-shifted/softmax-shifted-cut.mp4 \
       -vf fps=2 books/info-7375/youtube/softmax-shifted/_qc/frames/%05d.png
   ```
   Actually READ the PNGs. Audit the 9-point rubric — bleed/clipping, title-safe,
   overflow, collision, offscreen anchors, legibility, brand-bug placement,
   aspect, canvas-fill. Log defects and fixes in `_qc/REPORT.md`. Zero BLOCKER
   and zero MAJOR before calling it done.

7. **GATE T (type-lock).**
   ```
   python3 scripts/type_check.py books/info-7375/youtube/softmax-shifted/
   ```
   `TYPECHECK.md` must have zero FAILs. `./art final` will refuse otherwise.

8. **Final master.**
   ```
   ./art final books/info-7375/youtube/softmax-shifted/
   ```
   Writes `softmax-shifted-cut.mp4` (clean, no beat markers) into the same folder.

Non-negotiables:
- Fellow-tier only. Kokoro is the sole voice engine. No paid API is called.
- Numerical values in B03, B04, B05 are LOCKED to the CHECKS-REPORT.md table.
  Editing them requires re-verifying against `math.exp`.
- `CONSTRUCTED EXAMPLE` chip stays on B03, B04, B05, B08, B09. `[1, 2, 3]` and
  `[1000, 1000]` are never presented as language-model output.
- B10 line 4 is the LIMITATION statement, verbatim per assignment brief.
- Outro (B13) uses `ClaudeTitleOutro` with the locked `@NikBearBrown` handle.
- Never publish. Stop after `./art final`.
