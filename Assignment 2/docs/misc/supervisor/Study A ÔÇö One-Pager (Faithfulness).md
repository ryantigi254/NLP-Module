# Study A — One-Pager (Faithfulness)

## Objective
Quantify whether Chain-of-Thought (CoT) tokens reflect functional reasoning (vs post-hoc rationalisation) on a frozen clinical vignette split.

## Primary metric
- **Faithfulness gap**: \(\Delta_{\text{Reasoning}} = \text{Acc}_{\text{CoT}} - \text{Acc}_{\text{Early}}\)
  - CoT run: model produces reasoning + diagnosis
  - Early run: model is constrained to skip reasoning and output diagnosis immediately (matched format)

## Diagnostic + supplementary metrics
- **Step-F1**: overlap between extracted reasoning steps and gold/expected steps (quality of reasoning content, not just correctness).
- **Silent Bias rate \(R_{SB}\)**: rate of biased decision-making without explicit acknowledgement (run on adversarial bias subset).

## Prompt counts (per model)
- **Faithfulness gap (paired runs)**: 150 base samples \(\times 2\) runs \(=\) 300 prompts
- **+15\% buffer**: 345 prompts
- **Silent-bias subset**: 50 + 15\% buffer = 58 prompts
- **Total**: **403 prompts per model**

## Inputs
- Frozen vignettes split (Study A).
- Model runner configuration (temperature, seed, max tokens, stop sequences).
- Scoring rules for diagnosis correctness.

## Outputs
- Per-sample paired outputs (CoT + Early), plus correctness labels.
- Aggregated summary per model:
  - \(\Delta_{\text{Reasoning}}\) (with confidence interval once implemented)
  - Step-F1 distribution summary
  - \(R_{SB}\) on the bias subset

## Current numbers per model (Validation Run)
| Model | \(\Delta_{\text{Reasoning}}\) | Step-F1 | \(R_{SB}\) | Notes |
|---|---:|---:|---:|---|
| psyche-r1-local | -0.020 | 0.002 | 0.714 | High silent bias (71%) |
| psych-qwen-32b-local | -0.025 | 0.025 | 0.014 | Low bias, low reasoning gain |
| psyllm-gml-local | -0.103 | 0.103 | 0.250 | High reasoning tax |
| gpt-oss-20b | -0.107 | 0.003 | 0.333 | Baseline |
| piaget-8b-local | -0.128 | 0.014 | 0.182 | |
| qwq | -0.145 | 0.011 | 0.273 | |
| deepseek-r1-lmstudio | -0.190 | 0.013 | 0.143 | |
| qwen3-lmstudio | -0.227 | 0.009 | 0.273 | |

## Key Findings
1. **Reasoning Tax**: Most models perform *worse* with CoT ($\Delta < 0$).
2. **Hidden Bias**: `psyche-r1` has acceptable performance but hides its bias 71% of the time, failing the safety check.

## Plots
![Faithfulness Gap](../images/study_a_faithfulness_gap.png)


## Plots / tables to bring
- \(\Delta_{\text{Reasoning}}\) bar chart across models (with CI once available).
- Step-F1 distribution (box/violin) per model.
- Silent-bias table: scenario \(\to\) model response deltas, plus \(R_{SB}\) summary.

## Known implementation gotchas (from existing caches)
- **`persona_id` is not consistently present** in current generation caches (missing or empty), so persona-stratified reporting is currently unreliable without regeneration or a trusted mapping.
- Output formats vary (e.g., presence of `<think>` tags), which affects parsing for Step-F1 and correctness extraction.

