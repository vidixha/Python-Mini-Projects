
**W3 — Evaluation Metric Limitations and Lack of Stratified Analysis**

We thank the reviewer for this critique and present three complementary analyses that together address the concerns raised.

**1. Per-Cue-Type Stratified Evaluation**

We report Edit Exact Match (EEM) — a stricter metric that scores 1 only if the correct edit token appears *and* the struck-through original is absent — broken down by cue type across all evaluated models. Cue type membership is determined by IntentBench's ground-truth annotation flags. Rows marked † are statistically underpowered (N≤1) and excluded.

| Cue Type | DocIntentOCR-7B | DocIntentOCR-3B | Qwen2.5-VL-7B | Qwen2.5-VL-3B | GPT-4.1 | GPT-4o | o3 | Claude-Sonnet | Gemini-2.5-Flash | Gemini-2.5-Pro |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Strikethrough w/o Replacement | 0.8269 | **0.8462** | 0.6731 | 0.7885 | 0.7308 | 0.8269 | 0.8077 | 0.7115 | 0.8077 | 0.8269 |
| Table Column Deletion | 0.8137 | **0.8141** | 0.6913 | 0.6732 | 0.6942 | 0.8066 | 0.7107 | 0.7001 | 0.7194 | 0.6893 |
| Full Table Deletion | 0.6844 | 0.7142 | 0.7137 | 0.6833 | 0.7166 | 0.7982 | **0.8033** | 0.6765 | 0.6371 | 0.7056 |
| Strikethrough w/ Replacement | **0.7929** | 0.7677 | 0.5505 | 0.5657 | 0.7222 | 0.7828 | 0.7475 | 0.7020 | 0.6616 | 0.6162 |
| Arrow-Indicated Replacement | 0.7316 | 0.7526 | 0.5316 | 0.4368 | 0.6632 | 0.7632 | **0.7737** | 0.6947 | 0.6789 | 0.6421 |
| Table Cell Replacement | 0.8824 | 0.9412 | 0.8824 | 0.5882 | 0.8824 | **1.0000** | **1.0000** | **1.0000** | 0.8824 | 0.7059 |
| Caret Insertion | **1.0000** | **1.0000** | 0.8000 | 0.8000 | **1.0000** | **1.0000** | 0.6000 | **1.0000** | **1.0000** | 0.6000 |

DocIntentOCR-7B achieves the highest EEM on Strikethrough w/ Replacement — the most frequent cue type (209 instances, 185 documents) — outperforming all zero-shot models including GPT-4o and o3. This is the operationally most critical cue in financial document workflows.

**2. Edited vs. Non-Edited Region Analysis**

To directly address the concern about whether failures arise from incorrect intent interpretation versus spurious hallucination in unedited regions, we decompose performance into two components: Edited Region F1 (correctness of applied edits) and Non-Edited Region F1 (preservation of unmodified content).

| Model | Edited Region F1 | Non-Edited Region F1 |
| --- | --- | --- |
| DocIntentOCR-7B | 0.8656 | 0.8170 |
| DocIntentOCR-3B | 0.8667 | **0.8321** |
| Qwen2.5-VL-7B | 0.7312 | 0.7337 |
| Qwen2.5-VL-3B | 0.6753 | 0.7073 |
| GPT-4.1 | 0.8269 | 0.6815 |
| **GPT-4o** | **0.8677** | 0.8206 |
| o3 | 0.8634 | 0.8052 |
| Claude-Sonnet | 0.8398 | 0.6888 |
| Gemini-2.5-Flash | 0.8129 | 0.7145 |
| Gemini-2.5-Pro | 0.7667 | 0.6938 |

Two findings stand out. First, DocIntentOCR-7B matches GPT-4o on edited region F1 (0.8656 vs 0.8677) while using orders of magnitude fewer parameters and operating fully on-premise. Second, DocIntentOCR-3B achieves the highest non-edited region F1 (0.8321) across all models — demonstrating that intent-aware supervision teaches the model not only what to change but also what to preserve, reducing spurious hallucination in unedited content.

**3. Qualitative Error Analysis**

We identify three failure modes in DocIntentOCR-7B outputs: (i) systematic failures on arrow-indicated replacements spanning multiple table cells, where the model correctly identifies the arrow but applies the replacement to the wrong scope; (ii) near-miss cases where the correct replacement value is produced but the struck-through original is not fully suppressed; (iii) spurious hallucination in document footers and source metadata fields, which are not annotated and thus penalize the model despite being outside the task scope.

These analyses will be incorporated as a dedicated subsection in the revised submission. We respectfully ask the reviewer to reconsider the Soundness and Overall Assessment scores in light of this additional evidence.

