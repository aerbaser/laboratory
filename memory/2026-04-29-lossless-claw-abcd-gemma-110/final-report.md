# Gemma full 110 — merged report

Date: 2026-04-29
Model: `gemma4-31b` local via llama.cpp endpoint `127.0.0.1:8089`

## What this is
Live LLM answer-eval over harness-generated A/B/C/D contexts. It is not a full production OpenClaw e2e chat-compaction test.

## Methodology
- Fixture: 110 synthetic long-chat probes.
- A: sliding tail baseline.
- B: Lossless context using harness `CompactionEngine`.
- C: simulated OpenClaw memory retrieval.
- D: B + C combined.
- Merged from old 70-probe partial plus resumed 40-probe remainder.

## Sources
- `gemma-256-partial.json`: 70 probes
- `gemma-resume-70-110/live-raw-results.json`: 40 probes
- merged total: **110/110**

## Overall accuracy
- modeA: **0/110 = 0.0%**
- modeB: **58/110 = 52.7%**
- modeC: **60/110 = 54.5%**
- modeD: **44/110 = 40.0%**

## Accuracy by category
### conflict
- modeA: 0/15 = 0.0%
- modeB: 7/15 = 46.7%
- modeC: 14/15 = 93.3%
- modeD: 0/15 = 0.0%
### long
- modeA: 0/25 = 0.0%
- modeB: 25/25 = 100.0%
- modeC: 22/25 = 88.0%
- modeD: 24/25 = 96.0%
### multihop
- modeA: 0/20 = 0.0%
- modeB: 7/20 = 35.0%
- modeC: 7/20 = 35.0%
- modeD: 6/20 = 30.0%
### noise
- modeA: 0/10 = 0.0%
- modeB: 9/10 = 90.0%
- modeC: 7/10 = 70.0%
- modeD: 5/10 = 50.0%
### stale
- modeA: 0/10 = 0.0%
- modeB: 10/10 = 100.0%
- modeC: 10/10 = 100.0%
- modeD: 9/10 = 90.0%
### verbatim
- modeA: 0/30 = 0.0%
- modeB: 0/30 = 0.0%
- modeC: 0/30 = 0.0%
- modeD: 0/30 = 0.0%

## Caveats
- C/D memory path is simulated retrieval, not production Active Memory/Voyage/wiki e2e.
- Qwen was an accidental historical partial and is excluded from main comparison.
- Spark was blocked/unavailable and is excluded from main comparison.
- `gpt-5.4-mini` full 110 is still running separately at report creation time.