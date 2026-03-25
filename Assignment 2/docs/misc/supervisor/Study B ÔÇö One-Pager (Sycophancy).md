# Study B — One-Pager (Sycophancy)

## Objective
Measure whether a model shifts towards agreement with an incorrect user belief under social pressure, and whether it hallucinates evidence to justify that agreement.

## Primary metric
- **Sycophancy probability / agreement shift**:
  - Compute agreement rate under **injection** vs **control**, on matched prompts.
  - Report \(P_{\text{syc}}\) (agreement shift under injection).

## Diagnostic + advanced metrics
- **Evidence Hallucination \(H_{Ev}\)**: fraction of response claims not supported by the vignette (NLI-style check / claim-faithfulness pipeline).
- **Flip rate**: fraction of cases where control was correct, injected becomes incorrect.
- **Advanced (if implemented)**:
  - Truth Decay Rate (multi-turn accuracy slope)
  - Turn-of-Flip (first turn where the model fails)
  - Stance Shift Magnitude (ordinal stance delta)

## Prompt counts (per model)
- Single-turn control + injected:
  - 300 base samples \(\times 2\) runs \(=\) 600 prompts
  - +15\% buffer: 690 prompts
- Multi-turn “turn-of-flip” (if used):
  - 60 cases \(\times\) 5 turns = 300 prompts
  - +15\% buffer: 345 prompts
- **Total**: **1,035 prompts per model**

## Inputs
- Frozen opinion-injection prompt pairs (control/injected).
- Agreement detector specification (string/regex + optional classifier).
- Claim extraction + NLI/faithfulness checker configuration for \(H_{Ev}\).

## Outputs
- Per-pair outputs (control vs injected) with:
  - agreement label
  - correctness label (if available)
  - hallucination score / unsupported-claim count
- Aggregated per model:
  - \(P_{\text{syc}}\)
  - Flip rate
  - \(H_{Ev}\)
  - (Optional) ToF / TDR / SSM

## Current numbers per model (Validation Run)
| Model | \(P_{\text{syc}}\) | Flip rate | \(H_{Ev}\) | ToF | Notes |
|---|---:|---:|---:|---:|---|
| qwen3-lmstudio | -0.040 | 0.000 | 0.000 | 5.0 | Robust |
| gpt-oss-20b | -0.062 | 0.000 | 0.000 | 5.0 | Robust |
| psyllm-gml-local | -0.087 | 0.000 | 0.000 | 5.0 | Robust |
| piaget-8b-local | -0.098 | 0.000 | 0.000 | 5.0 | Robust |
| psych-qwen-32b-local | -0.109 | 0.000 | 0.000 | 5.0 | Robust |
| qwq | -0.116 | 0.000 | 0.000 | 5.0 | Robust |
| psyche-r1-local | -0.126 | 0.000 | 0.000 | 5.0 | Robust |
| deepseek-r1-lmstudio | -0.162 | 0.000 | 0.000 | 5.0 | Robust |

## Key Findings
1. **High Robustness**: No model flipped to the incorrect diagnosis ($H_{Ev} = 0.0$).
2. **Negative P_Syc**: All models showed *negative* sycophancy (disagreed more when pressured), indicating strong safety training.

## Plots
![Sycophancy Probability](../images/study_b_sycophancy_prob.png)
![Sycophancy vs Hallucination](../images/study_b_syc_vs_hav.png)


## Known implementation gotchas (from existing caches)
- **Locale leakage**: some outputs include US-specific hotline references (e.g., “988”, “U.S.”), which is undesirable for UK-focused personas and can bias qualitative interpretation.
- **`persona_id` is not consistently present** in current generation caches (missing or empty), so persona-stratified reporting is currently unreliable without regeneration or a trusted mapping.

