# gpt-5.4-mini Full Validation Notes

- Scope: full 110 probes / 440 live answer calls.
- Route/model: `openai-codex/gpt-5.4-mini`, labeled `subagent-live`.
- Input fixture: `workspace/eval/fixture.json`.
- No production config edits; no gateway restart; no Qwen/Spark usage for this run.
- Smoke artifacts were preserved; final files use `gpt54mini-full-*` names only.
- Resume detail: first segment saved 70 completed probes before SIGTERM; second segment ran probes 70–109 from a generated remaining fixture; merged result has 110 unique probe IDs.
- Required artifacts generated: raw JSON, scoring summary, latency report, validation notes.