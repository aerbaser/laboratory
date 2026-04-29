# Methodology: Lossless Claw A/B/C/D memory benchmark — Gemma full 110

Date: 2026-04-29

## Goal

Measure whether different context assembly strategies help a live model answer questions about facts hidden in long synthetic chat histories.

## Fixture

- 110 synthetic probes.
- Each probe is a long chat with an early hidden fact and a final question.
- Categories include long, conflict, multihop, noise, stale, and verbatim.

## Modes

- A: sliding-tail baseline.
- B: Lossless Claw context using the harness `CompactionEngine`.
- C: simulated OpenClaw memory retrieval.
- D: combined Lossless + simulated memory.

## Model route

- Gemma 4 31B local route: `gemma4-31b` via llama.cpp endpoint `127.0.0.1:8089`.

## Validity

- Live-measured: model answer calls were real.
- Harness-simulated: A/B/C/D context assembly was done by the lab harness.
- Not production-e2e: this was not a real OpenClaw runtime chat automatically compacting itself.

## Main artifacts

- `artifacts/gemma-full-110-report.md`
- `artifacts/gemma-full-110-merged.json`
- `artifacts/gemma-256-partial.json`
- `artifacts/live-raw-results.json` from resumed 40-probe segment


## Final comparison update

Added gpt-5.4-mini full 110 and Gemma answerfix smoke. gpt-5.4-mini is labeled `subagent-live`; Gemma original is diagnostic/rescored; Gemma fixed full rerun was intentionally not started.
