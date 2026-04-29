# Live Scoring Summary — A/B/C/D

Stage: **full** (110 probes)
Model: `openai-codex/gpt-5.4-mini` via subagent-live proxy `http://127.0.0.1:18054`
Context budget per call: 20000 tokens
Total LLM calls: 440
Total measured LLM latency: 5003.0s

## Overall recall (110 probes; live answer step)

| Mode | Hits | Recall | Wilson 95% CI | Avg latency (s) |
|---|---:|---:|---|---:|
| A | 2/110 | 1.8% | [0.5%, 6.4%] | 12.9 |
| B | 108/110 | 98.2% | [93.6%, 99.5%] | 11.3 |
| C | 110/110 | 100.0% | [96.6%, 100.0%] | 11.1 |
| D | 109/110 | 99.1% | [95.0%, 99.8%] | 10.3 |

## Per-category recall

| Category | n | A | B | C | D |
|---|---:|---:|---:|---:|---:|
| long | 25 | 0/25 (0%) | 25/25 (100%) | 25/25 (100%) | 25/25 (100%) |
| conflict | 15 | 0/15 (0%) | 14/15 (93%) | 15/15 (100%) | 15/15 (100%) |
| stale | 10 | 2/10 (20%) | 10/10 (100%) | 10/10 (100%) | 10/10 (100%) |
| noise | 10 | 0/10 (0%) | 9/10 (90%) | 10/10 (100%) | 10/10 (100%) |
| multihop | 20 | 0/20 (0%) | 20/20 (100%) | 20/20 (100%) | 20/20 (100%) |
| verbatim | 30 | 0/30 (0%) | 30/30 (100%) | 30/30 (100%) | 29/30 (97%) |

## Privacy leakage (cat=noise) — live answer text

| Mode | Leaks | Rate |
|---|---:|---:|
| A | 0/10 | 0% |
| B | 0/10 | 0% |
| C | 0/10 | 0% |
| D | 0/10 | 0% |

## Stale-fact bleed (cat=conflict + cat=stale)

| Mode | Leaks | Total |
|---|---:|---:|
| A | 0/25 | 0% |
| B | 0/25 | 0% |
| C | 0/25 | 0% |
| D | 0/25 | 0% |

### Notes
- Label: **subagent-live**. This used the local gpt54mini OpenAI-compatible proxy, which calls `openclaw infer model run --gateway --model openai-codex/gpt-5.4-mini`.
- A/B/C/D semantics preserved: A sliding tail baseline; B CompactionEngine + lcm_grep-style retrieval; C simulated OpenClaw memory retrieval; D combined.
- Full run was merged from a 70-probe checkpoint plus a 40-probe resume after the first process received SIGTERM; probe IDs are unique and cover `long-0` through `verbatim-109`.