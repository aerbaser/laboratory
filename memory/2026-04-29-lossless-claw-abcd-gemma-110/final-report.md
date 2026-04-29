# Final comparison: Lossless Claw A/B/C/D memory benchmark

Date: 2026-04-29

## Executive verdict

Do **not** treat this as production-e2e proof yet. Treat it as strong harness evidence that Lossless/Memory-style context assembly is valuable and worth installing for a guarded pilot/evaluation, not as a blind production rollout.

Recommendation: **install/pilot behind a feature flag or isolated profile**, then run a real OpenClaw production-e2e chat compaction test before making it default.

## Main result: gpt-5.4-mini full 110

- Label: `subagent-live`
- Probes: **110/110**
- Live calls: **440**
- Noise leaks: **0**
- Stale leaks: **0**

- A baseline: **2/110 measured = 1.8%**
- B Lossless: **108/110 measured = 98.2%**
- C simulated memory: **110/110 measured = 100.0%**
- D combined: **109/110 measured = 99.1%**; **109/109 answered = 100%** (1 infra/runtime failed call)



### Denominator note

Scores with transport/runtime failures must not be interpreted as semantic wrong answers. The primary table keeps the measured denominator (`/110`) for reproducibility, but quality interpretation should use answered-call denominator when a mode failed before producing content. For gpt-5.4-mini D, the single miss was `verbatim-108` with HTTP 500 / empty content; B and C answered that same probe correctly. Therefore D is **109/110 measured**, but **109/109 answered correctly**.

## Gemma evidence

Gemma original full 110 was diagnostic because many correct values were emitted in `thinking` while final `content` was empty/truncated. Rescoring `content+thinking` gives:

- A baseline: **7/110 = 6.4%**
- B Lossless: **77/110 = 70.0%**
- C simulated memory: **77/110 = 70.0%**
- D combined: **76/110 = 69.1%**

Gemma answerfix smoke validated the fix (`ANSWER`/JSON content, larger output budget):
- A baseline: **0/12 = 0.0%**
- B Lossless: **12/12 = 100.0%**
- C simulated memory: **9/12 = 75.0%**
- D combined: **12/12 = 100.0%**

## Validity

- `live-measured`: model calls were real for Gemma and gpt-5.4-mini.
- `harness-simulated`: A/B/C/D context assembly/retrieval was performed by the harness.
- Not `production-e2e`: this did not prove real OpenClaw runtime automatic chat compaction yet.
- Qwen is obsolete accidental partial; Spark is blocked/unavailable.

## Decision

Use the tool for a controlled pilot. The harness result is strong: baseline is near-zero while Lossless/Memory/Combined are near-perfect on gpt-5.4-mini. But before default install, require one production-e2e validation: real session filled with messages → automatic compaction/memory hooks → final questions → report.


## Production-path Gemma e2e update

A separate isolated production-path e2e was run with real `openclaw agent` turns, noise turns, `/compact`, then post-compaction control questions.

Result: **6/6 PASS**.

This is stronger evidence than the A/B/C/D harness that OpenClaw+Gemma can preserve exact early facts through real session compaction in an isolated profile. It is still not a long-running main Telegram production soak, but it clears the first production-path gate.
