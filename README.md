---
schema_version: "1.0"
type: eem
project_name: "reasons"
domain: []
license: mit
base_network: null
source_repos: []
beliefs_total: 494
beliefs_in: 431
beliefs_out: 63
premises: 134
derived: 360
nogoods: 0
generator: ftl-reasons/0.48.0
---

# Reasons

## Stats

| Metric | Value |
|--------|-------|
| Total beliefs | 494 |
| Status | 431 IN / 63 OUT |
| Premises (observations) | 134 |
| Derived (justified conclusions) | 360 |
| Nogoods (contradictions) | 0 |
| Retraction rate | 13% |
| Max derivation depth | 18 |

## How to Use

### Import into a reasons database

```bash
reasons init
reasons import-json network.json
```

### Query beliefs

```bash
reasons search "your query"
reasons explain <node-id>
reasons show <node-id>
```

## Files

| File | Description |
|------|-------------|
| `network.json` | Full belief network (machine-readable, portable) |
| `reasons.db` | SQLite database (gitignored, regenerate with `reasons import-json network.json`) |
| `README.md` | This EEM card |

## Quality

- 431 beliefs IN, 63 OUT
- 134 premises grounded in direct observations
- 360 derived beliefs justified via SL justifications
- 0 nogoods detected

## Exam Results

40-question exam across 16 objectives, tested on 3 models in 3 conditions:
- **beliefs**: all 431 IN beliefs provided as context
- **control**: no beliefs (model's own knowledge only)
- **agentic**: model uses `search_beliefs` tool to query the EEM

| Model | With Beliefs | Control | Agentic | Delta |
|-------|-------------|---------|---------|-------|
| claude:opus | 40/40 (100%) | 37/40 (92%) | 40/40 (100%) | +8% |
| claude:sonnet | 40/40 (100%) | 37/40 (92%) | 39/40 (97%) | +8% |
| claude:haiku | 39/40 (97%) | 36/40 (90%) | 35/40 (87%) | +7% |

The EEM consistently improves accuracy by +7-8% across all model tiers, with the largest gains on obscure historical facts (GMDH as first DL algorithm 1965, transfer learning dating to 1976) and nuanced claims (batchnorm ICS explanation being challenged). See `results/matrix-summary.md` for the full per-objective breakdown.

## Limitations

- Auto-generated card — review and customize for your use case

## License

mit
