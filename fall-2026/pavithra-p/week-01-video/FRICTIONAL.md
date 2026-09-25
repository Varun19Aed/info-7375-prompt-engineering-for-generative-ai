# Frictional — Week 01 video

Pavithra Prasad. · INFO 7375 · Week 01 video ("Thousands of Years, Divided")

> **How this log was written:** events are dated on the day they happened. On 2026-09-25 I reorganised the log into the course's entry format with Claude's help, because my first version described Claude's technical fixes as if I had done them. The parts marked *[in my words]* are mine.

---

## 2026-09-22 — Understanding the assignment and picking a topic

- **I tried:** reading the brief and asking Claude for a plan. I asked which Chapter 1 topic would be easy to explain and still meet the rubric.
- **What happened:** Claude listed the eligible topics. It recommended "subtracting the maximum" (Part 2) first, then "expected 665.24 vs observed 630" (Part 2) as the easiest.
- **What I did:** I picked the 665.24 vs 630 topic and asked Claude to check it against the rubric before going further.
- **What Claude contributed:** the topic list, a rubric comparison, and a real run of `lessons/01-.../code/main.py` (counts 102 / 268 / 630 at seed 7). It also found that seed 7 is the lowest of seeds 0–99.
- **I expected / still wondered:** *[in my words — e.g. what I expected the assignment to take, or what I was unsure about at this point]*

## 2026-09-23 — Switching from Part 2 to Part 1

- **Friction:** when I read the Part 2 beat sheet and the explanation of the 8 beats, I could not follow it. It was too many probabilities for me to defend every claim, and the rubric requires that.
- **What I did:** I said so, and asked whether a Part 1 topic could still score well. I chose **"a training-scale slogan restated as a division with a hidden assumption"** because it only needs multiplication and division.
- **What Claude contributed:** a comparison of the Part 1 topics against the rubric, and a run of `research/llm_scale.py` confirming the chapter's numbers (1,426.0 / 1,711.2 / 2,138.9 / 2,851.9 years). It also suggested an extra hidden assumption: reading 24 hours a day.
- **Accepted / changed:** I accepted the Part 1 topic and the 8-hours-a-day extension, on condition it is labelled on screen as an extension. The Part 2 draft files were deleted, not submitted.
- **Evidence:** `evidence.py`, `evidence.json`.

## 2026-09-23 — Reviewing the beat plan and narration

- **I tried:** reading the beat plan and full narration before any audio was made.
- **What I did:** I brought a set of wording suggestions and asked Claude whether to use them: B01 ("reported starting number"), B02 ("the chapter's approximation"), B04, B05 (label the extension clearly) and B06 (the unique-tokens limit). I skipped the Claude-screen opening, since it would need a real, dated Claude response.
- **Changed, not just accepted:** Claude agreed with them but reworded one. For B04 it pointed out that "a difference of 1,426 years" would sound identical to the 300-wpm answer (also 1,426), so we used "the slowest reader's answer is twice the fastest" instead.
- **Two corrections I required before approving:**
  - B00: "It isn't a measurement" → "an estimate produced by division". The 300 billion tokens is *reported*; only the reading time is *estimated*.
  - B06: "describes how much text went in" → "translates a reported training-token count into hypothetical human reading time". The old line contradicted the sentence before it.
- **Also caught:** Claude said the script was ~450 words. The real count was 393 (~2:30).
- **Evidence:** `beat_sheet.json` → `metadata.review` (approved 2026-09-23).

## 2026-09-23 — Tool problems (Claude Code handled these; I followed along)

I asked Claude to build the video and not commit or push anything. It hit these problems and handled them.

- Homebrew refused to install ffmpeg because of an unrelated MongoDB tap on my Mac. Claude skipped that check with environment flags instead of changing Homebrew's trust settings.
- Manim needed the cairo/pango libraries (`brew install cairo pkg-config pango`).
- Brutalist's `./setup` stopped on its own example files ("ElevenLabs reference found"). Claude ran the same readiness checks by hand; the Kokoro voice test passed.
- The toolkit's quality gates rejected scenes several times: text a hair past the margin, too much empty space mid-scene, overlapping captions. Each was fixed and only that scene re-rendered.
- **I asked:** whether all of this was free (yes: Kokoro, Manim and ffmpeg run locally; $0), and what Claude had installed or changed outside my folder (listed in chat; nothing in the course repo was edited).
- **What I don't fully understand:** *[in my words — e.g. how the quality gates decide something is "off-frame", or anything else here you'd want to learn]*

## 2026-09-24 — I spotted uneven letter spacing

- **What happened:** watching the video full screen, I noticed gaps inside words: "slo gan", "parap hrased", "co urse". None of the automated checks had caught it, and neither had Claude's frame check.
- **What I did:** I sent a screenshot and asked about it. I also asked whether I needed an intro (Claude said no: B00 already works as one, and extra time would be padding).
- **What Claude contributed:** the cause (a known Manim text-spacing issue at small sizes) and the fix (render text 4× larger, then shrink it). In the same round it flipped the B04 slider to match the bar order and added my name under the title.
- **Decision:** I asked for all fixes in one round and said this would be the last version.
- **Evidence:** before/after frames of B00; final `thousands-of-years-divided.mp4` (2:28).

## 2026-09-25 — Comparing with another video, and final checks

- **I tried:** giving Claude another Week 1 video (on softmax) and asking for an honest comparison and grades for both.
- **What I learned from it:** the other video showed the program's raw printed output as evidence, which is strong. It was also the review copy with debug labels burned in, which is why exporting the clean final version matters.
- **Decision:** I kept my video unchanged. Claude said no changes were needed, and cautioned against borrowing another video's structure or wording.
- **Cleanup:** Claude deleted about 155 MB of build leftovers and some Python cache folders. I asked whether this log read as AI-written. Claude pointed out that my first version described its technical fixes as mine, so I asked it to reorganise the log in the course format.

---

## What I understand now

*[in my words — 3–5 bullets. For example: why "thousands of years" is a division and not a measurement; which three guesses are hidden in it; why halving reading speed doubles the years; what the calculation cannot tell you.]*

-
-
-

## What I still don't understand / next step

*[in my words — 1–3 bullets. For example: something about tokens, how GPT-3's 300B figure was counted, whether tokens were repeated in training, or something about the tools.]*

-
-
