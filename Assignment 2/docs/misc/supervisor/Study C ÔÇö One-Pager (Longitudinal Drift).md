# Study C — One-Pager (Longitudinal Drift)

## Objective
Measure whether a model maintains a consistent patient representation over long, multi-turn interactions (entity retention + contradiction avoidance).

## Primary metric
- **Entity Recall (target \(> 0.7\))**:
  - Extract critical entities from initial context (Turn 1).
  - Measure how many are still recoverable/mentioned in later turns (or in a requested summary).

## Diagnostic + supplementary metrics
- **Knowledge Conflict \(K_{\text{conflict}}\)**: contradiction rate between adjacent turns (Dialogue NLI-style).
- **Continuity score**: similarity between model actions and a target care plan (embedding cosine similarity).
- **Advanced (if implemented)**:
  - PDSQI-9 quality scoring via judge/rubric (very high cost)
  - Drift rate as slope over turns/tokens (requires token tracking)

## Prompt counts (per model)
- 40 multi-turn cases \(\times\) 10 turns = 400 prompts
- +15\% buffer: 460 prompts
- **Total**: **460 prompts per model**

## Inputs
- Frozen multi-turn scripts (Study C).
- Entity extraction configuration (clinical NER model + label set).
- NLI model selection + thresholds for contradiction classification.

## Outputs
- Per turn:
  - entity set extracted from response/summary
  - recall-at-turn \(t\)
  - contradiction verdict(s) for adjacent turns
- Aggregated per model:
  - entity recall curve
  - mean recall at final turn (e.g., Turn 10)
  - \(K_{\text{conflict}}\) summary

## Current numbers per model (Validation Run)
| Model | Recall@T10 | Mean recall | \(K_{\text{conflict}}\) | Notes |
|---|---:|---:|---:|---|
| psyllm-gml-local | 0.715 | 0.881 | 0.004 | Best retention (Expert) |
| psyche-r1-local | 0.537 | 0.545 | 0.005 | Moderate retention |
| qwen3-lmstudio | 0.518 | 0.869 | 0.042 | High decay |
| qwq | 0.491 | 0.668 | 0.033 | |
| gpt-oss-20b | 0.432 | 0.770 | 0.016 | |
| psych-qwen-32b-local | 0.374 | 0.616 | 0.000 | Low recall |
| deepseek-r1-lmstudio | 0.366 | 0.895 | 0.033 | Worst retention |

## Key Findings
1. **Domain Advantage**: `psyllm` (expert) significantly outperforms generalist models in long-context retention.
2. **Reasoning Decay**: `deepseek-r1` starts strong (Acc 89%) but forgets 64% of details by Turn 10.

## Plots
![Recall @ T10](../images/study_c_recall_t10.png)


## Known implementation gotchas (from existing caches)
- **`persona_id` is not consistently present** in current generation caches (missing or empty), so persona-stratified reporting is currently unreliable without regeneration or a trusted mapping.

