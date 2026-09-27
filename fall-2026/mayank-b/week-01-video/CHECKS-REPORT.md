# CHECKS-REPORT (written before the first render)

8 SHOW / 0 justified-HOLD / 0 PUNT-flagged (body B01A–B08; B01A added in v5); 5 bookends.

Teaching arc: FRAMEWORK ✓ (B02 softmax) | WORKED EXAMPLE ✓ (B03–B04 real numbers)
| FALSIFIABILITY ✓ (B07 constructed wrong-answer case) | SCAFFOLDED TASK ✓ (BHTF prompt)
| BOOKENDS ✓ (B00, B01, BVDT, BHTF, BOUT) | NO-SOURCE-NO-VERDICT ✓ (verdict lines trace to FACTCHECK.md)

Deliberate deviations (logged, not silent):
- ASK→RESULT micro-beats omitted: showing typed Claude prompts before each graphic would
  imply Claude generated them; the assignment forbids implying Claude output that did not
  happen. The graphics come from local code, stated on screen.
- B00 composer "output" lines are the program's stdout, prefixed `$ python3 run_temperature.py`.
