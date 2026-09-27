# Friction Log

**Student:** Varun Tadimeti  
**Course:** INFO 7375  
**Assignment:** Week 1 Video  
**Project:** Softmax, Shifted

This document records the main points of friction encountered while building the Week 1 video, along with the actions taken to resolve them.

## 2026-09-26 — 1. Brutalist and Claude Code Workflow

**Friction:** At the beginning of the project, I was unsure about the difference between using Claude Code locally and the browser/cloud interface, including whether GitHub access was required.

**Response:** I used the locally cloned Brutalist repository and ran Claude Code from inside the repository. The public Brutalist repository could be inspected locally without giving Claude access to my GitHub account.

**Lesson:** Separating the local development environment from cloud integrations made the workflow easier to understand.

## 2026-09-26 — 2. Kokoro Narration Setup

**Friction:** The first narration-generation attempt failed because the required Kokoro package was not available in the environment.

**Response:** I installed the required local Kokoro dependency and continued using Kokoro for narration.

**Lesson:** The narration pipeline depends on local environment setup even though it does not require a paid API.

## 2026-09-26 — 3. ElevenLabs Warning

**Friction:** Brutalist setup reported references to ElevenLabs even though this assignment required the free/local Kokoro narration workflow.

**Response:** I did not install or use ElevenLabs. The final narration was generated with Kokoro.

**Lesson:** Repository warnings can refer to older or example files and do not necessarily describe the actual production pipeline.

## 2026-09-26 — 4. Python / Manim Compatibility

**Friction:** A broader setup attempt encountered a compatibility issue involving Python 3.13 and the pinned Manim environment.

**Response:** I avoided making Manim a dependency for the final algebra scene. Mathematical expressions were instead typeset as SVG using Matplotlib and animated with Remotion.

**Lesson:** When one rendering dependency creates environment conflicts, it can be better to use another supported local rendering path rather than destabilizing the whole project.

## 2026-09-26 — 5. FFmpeg Dependency

**Friction:** FFmpeg was initially missing from the local environment.

**Response:** I installed FFmpeg with Homebrew and then used it for video/audio assembly and inspection.

**Lesson:** Video-generation workflows often rely on system-level tools in addition to Python and JavaScript packages.

## 2026-09-26 — 6. Template Attribution

**Friction:** The initial Brutalist template included the `claude-liam` persona and Nik Bear Brown channel branding. Because this was a student assignment, I did not want the narration to imply that the professor was presenting my work.

**Response:** Spoken references to Liam were removed from the narration. A separate student credit beat was added:

`INFO 7375 · Northeastern University`

`Varun Tadimeti · Week 1`

The locked Brutalist/Nik Bear Brown template branding was otherwise preserved.

**Lesson:** Template branding and assignment authorship need to be treated separately.

## 2026-09-26 — 7. Gate F During Previsualization

**Friction:** An early `./art run` was stopped because Gate F required `FACTCHECK.md`, `SHOTLIST.md`, and `PROMPTS.md`.

**Response:** A preview-only bypass was used while the video was still being developed. Before finalization, the required documentation was created and the fact-check validation passed.

**Lesson:** Preview shortcuts should remain temporary; final builds need the full provenance and verification documentation.

## 2026-09-26 — 8. Placeholder Scenes

**Friction:** Several beats initially used placeholder SLATE scenes, which made the previsualization structurally complete but visually incomplete.

**Response:** The important mechanism beats were replaced with custom Remotion scenes, including the softmax recipe, direct-versus-shifted comparison, algebra derivation, and extreme-value stability example.

**Lesson:** Previsualization is useful for timing and structure, but mechanism-heavy educational content needs purpose-built visuals.

## 2026-09-26 — 9. Algebra Scene

**Friction:** The algebra scene originally depended on the Manim path, which was inconvenient because of the environment conflict.

**Response:** I created a custom `SoftmaxDerivation` Remotion scene and used Matplotlib-generated SVG equations. The scene progressively reveals the equations and demonstrates cancellation of the common factor.

**Lesson:** The important requirement was to visibly show the mechanism; the exact rendering library was secondary.

## 2026-09-26 — 10. Claude Code Rate Limit

**Friction:** Claude Code reached a usage/rate limit while the project was still being finalized.

**Response:** I continued the remaining debugging and build workflow manually in Terminal with ChatGPT assistance rather than waiting for Claude Code.

**Lesson:** Keeping the project understandable and runnable locally made it possible to continue even when one AI tool became unavailable.

## 2026-09-27 — 11. Gate V Visual QC

**Friction:** Automated visual QC initially found real layout problems, including B01 edge bleed and bottom-safe-area problems in B06 and B09.

**Response:** The B01 typography was reduced to fit safely, and the B06/B09 bottom labels were moved upward. After these changes, Gate V reported zero BLOCKER defects.

**Lesson:** Automated QC was useful for finding genuine layout problems that were easy to miss during implementation.

## 2026-09-27 — 12. Gate T Contrast and Minimum-Size Checks

**Friction:** Gate T identified low-contrast accent text and minimum-size failures in several custom scenes.

**Response:** The low-contrast text was changed to the darker ink color and small labels were increased in size. The remaining minimum-size detections were inspected using diagnostic frames.

**Lesson:** Automated accessibility checks should be followed by visual inspection to determine whether a reported component actually represents designed text.

## 2026-09-27 — 13. Connected-Component False Positives

**Friction:** After increasing the relevant font sizes, Gate T continued reporting tiny 8px/16px components in B02, B04, and B09.

**Response:** Diagnostic frames showed that the detected components were arrow geometry or fragments of otherwise correctly sized glyphs rather than intentionally undersized text. A narrowly scoped project-specific §8.1 false-positive declaration was added for those three verified patterns. Other Gate T checks remained active.

**Lesson:** A quality gate should not be disabled globally because of a false positive. Exceptions should be narrow, documented, and based on manual inspection.

## 2026-09-27 — 14. Intentional Negative Space

**Friction:** Final Gate V reported six MAJOR `underfill` findings: two frames each from B01, B07, and B11.

**Response:** Each scene was manually reviewed. B01 intentionally uses a sparse BLUF statement, B07 leaves space around the mathematical derivation for readability, and B11 is intentionally a minimal assignment credit card. Brutalist's built-in per-beat `qc.sparse_by_design` mechanism was used with a written reason for each beat. Only the underfill/clustered checks were waived; other visual checks remained active.

**Lesson:** Negative space can be intentional. The toolkit's per-beat exception mechanism allowed that design decision to be documented without globally weakening visual QC.

## 2026-09-27 — 15. Hidden Final-QC Output

**Friction:** When the final build first failed, the compile helper displayed the failed `final_frame_check.py` command but hid the detailed Gate V output because stdout was captured.

**Response:** The compile helper was temporarily adjusted to expose captured stdout. This revealed that the only remaining findings were the six known underfill warnings.

**Lesson:** Build tooling should expose enough diagnostic information to distinguish a rendering failure from a quality-control decision.

## Final Result

The final command:

`./art final books/info-7375/youtube/softmax-shifted/`

completed successfully.

The final build reported:

- Gate T: PASS
- 14/14 beats filled
- Runtime: approximately 173.3 seconds
- Final master: `renders/softmax-shifted.mp4`

The final video was manually reviewed in addition to the automated quality-control process.
