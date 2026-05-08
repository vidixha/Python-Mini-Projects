# Survey V2: Default vs Deepresearch

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **Use Case** | Fast iteration during exploration | Final methodology decision before Setup phase |
| **Tools Used** | HF Papers, arXiv, HF Datasets, GitHub, WebSearch | Same tools + enhanced tracking |

---

## Citations & Verification

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **Insights Citations** | No citations | Inline [Author Year, arXiv:XXXXX](URL) on every bullet |
| **URL Verification** | No verification | 100% verified (curl -I -L) with HTTP status codes |
| **Citation Format** | Informal author references in text | Formal bracketed citations with arXiv IDs and URLs |
| **Model Card Links** | Listed but not verified | All verified; license tags confirmed on page |
| **Dataset Links** | Listed but not verified | All verified; MIT/Apache-2.0 confirmed |
| **Broken Links** | Possible | Caught and marked `[BLOCKED: 404]` |

---

## Benchmarks & Model Ranking

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **M Ranking** | Score on primary benchmark (inputs/benchmark.yaml) | Same as default |
| **M' Ranking** | Published leaderboard scores on same benchmark | Same as default |
| **Benchmark Comparison** | Unified table (all models, same benchmark, sorted by score) | Same as default |
| **Source Documentation** | M/M' rows have Source column but not linked | Source column has verified URLs |
| **Type Column** | OSS-small / OSS-large / Commercial | Same, but with evidence URLs |

---

## Artifacts Generated

| Artifact | Default Mode | Deepresearch Mode |
|----------|--------------|-------------------|
| `REPORT.md` | ✓ (7 required sections) | ✓ (7 sections + References section) |
| `survey-plan.md` | — | ✓ (research questions + evidence matrix) |
| `survey-evidence.md` | — | ✓ (query log + source disposition + rejection analysis) |
| `survey-verification.md` | — | ✓ (URL validation report with HTTP codes) |
| `survey-provenance.md` | — | ✓ (coverage table + verification status + confidence scoring) |
| `LAB.md` log entry | ✓ (M, M', benchmark used) | ✓ (sources consulted/accepted, verification status) |

---

## Evidence Tracking

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **Sources Tracked** | Not documented | Detailed: papers/models/datasets/benchmarks consulted vs accepted |
| **Rejection Reasons** | Not tracked | 8 categories documented with implications |
| **Rejection Rate** | Unknown | Explicit (e.g., "46 consulted → 18 accepted → 61%") |
| **Coverage Metrics** | None | Table: consulted/accepted per source type |
| **Quality Justification** | Implicit | Explicit: high rejection = rigorous gatekeeping |

---

## Confidence & Uncertainty

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **Finding Confidence** | Not scored | Labeled HIGH/MEDIUM/EMERGING with % confidence |
| **Uncertainty Quantification** | Implicit | Explicit: all findings ranked by evidence strength |
| **Paradigm Shift Documentation** | Mentioned | Detailed timeline (2022 pipeline → 2024-2025 VLM) |
| **Research Limitations** | Not documented | 7 constraints listed with impact assessment |
| **Overall Survey Confidence** | 100% (assumed) | 85% (documented constraints) |

---

## Report Enhancements

| Section | Default Mode | Deepresearch Mode |
|---------|--------------|-------------------|
| **Insights** | ✓ No citations | ✓ Inline citations [Author, arXiv:ID](URL) |
| **Benchmarks** | ✓ Name + version | ✓ + Verified? column + Source URL |
| **Datasets** | ✓ Name + size + license | ✓ + Evidence column (search tool + URL) |
| **M** | ✓ Rank/model/params/score/source/license | ✓ + verified source URLs |
| **M'** | ✓ Rank/model/score/source | ✓ + verified source URLs |
| **Benchmark Comparison** | ✓ Combined ranking table | ✓ Same table with verified URLs |
| **Methodology-hints** | ✓ Candidate methodologies with evidence | ✓ Same + risk assessment + confidence scores |
| **References** | — | ✓ NEW: deduplicated list (papers/models/datasets/benchmarks) with verification status |

---

## Quality Assurance

| Aspect | Default Mode | Deepresearch Mode |
|--------|--------------|-------------------|
| **Section Completeness** | ✓ (7 required sections) | ✓ (7 + References) |
| **License Validation** | ✓ (MIT or Apache-2.0) | ✓ + verified on resource page |
| **Citation Validation** | — | ✓ Every claim traceable to URL |
| **URL Reachability** | Not checked | ✓ All URLs verified 2xx/3xx + dates |
| **Deduplication** | Not tracked | ✓ References deduplicated by URL |
| **No Duplicates** | Not documented | ✓ Each URL appears once in References |
| **Source Attribution** | Informal | ✓ Formal: every table row has evidence URL |

---

## Exit Conditions

| Condition | Default Mode | Deepresearch Mode |
|-----------|--------------|-------------------|
| **7 Required Sections** | ✓ check_phase.sh validates | ✓ check_phase.sh validates |
| **License Tags** | ✓ check_phase.sh validates | ✓ check_phase.sh validates |
| **M Ranking** | ✓ Sorted by score on primary benchmark | ✓ Same |
| **M' Ranking** | ✓ Same benchmark as M | ✓ Same |
| **survey-plan.md** | — | ✓ Must exist |
| **survey-evidence.md** | — | ✓ Must exist with query log |
| **survey-verification.md** | — | ✓ Must exist with URL validation |
| **survey-provenance.md** | — | ✓ Must exist with coverage + verification |
| **Inline Citations in Insights** | — | ✓ ≥1 citation per Insights bullet |
| **References Section** | — | ✓ ≥10 unique sources, all verified |
| **LAB.md Entry** | ✓ M/M'/benchmark | ✓ + sources consulted/accepted/verification status |

---

## When to Use Each Mode

### Use Default Mode When:
- Early exploration phase (TASK discovery)
- Need quick model/dataset/benchmark snapshot
- Iterating on task definition
- Rapid prototyping (5–10 min surveys acceptable)
- Publishing not required yet

### Use Deepresearch Mode When:
- Final methodology decision before Setup phase
- Building publication-ready survey
- Need to justify model/dataset choices to stakeholders
- Want transparent uncertainty quantification
- Citation traceability required

---

## Example Output Sizes

| Artifact | Default Mode | Deepresearch Mode |
|----------|--------------|-------------------|
| REPORT.md | ~15–18 KB | ~18–25 KB (+ References section) |
| survey-evidence.md | — | ~6–8 KB |
| survey-verification.md | — | ~2–3 KB |
| survey-provenance.md | — | ~8–12 KB |
| **Total artifacts** | 1 file | 5 files |
| **Total size** | 15–18 KB | 35–55 KB |

---

## Key Difference Summary

**Default Mode:** Fast, tool-driven, no citations. Good for exploration.

**Deepresearch Mode:** Slow, source-grounded, 100% verified, production-ready. Good for final decisions.

**Both modes:** Same-benchmark requirement (M and M' ranked on identical OmniDocBench v1.0). Benchmark Comparison table included. License validation enforced.
