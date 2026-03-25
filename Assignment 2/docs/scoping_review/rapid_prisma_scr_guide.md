# Rapid PRISMA-ScR Scoping Review Guide (clinician-readable)

Last updated: 2026-02-18

This is the working guide for the scoping review paper that evidence-maps mental-health conversational AI/LLMs and positions the A/B/C benchmark (faithfulness, user-pressure/sycophancy, multi-turn drift).

## What changed in this revision (from the prompt version)

- Anchored the “Layer 2” methods-transfer set to the existing local literature pack (see “Local seed set”).
- Tightened mental-health search terms and exclusions (to avoid accidentally reviewing “general clinical LLM QA” papers that are not conversational mental-health dialogue).
- Elevated fairness/empathy/bias as an explicit secondary question (because it shows up in the local seed set and is clinically material).
- Added an explicit “known missing” call-out: the current local pack is strong for Layer 2, weak for Layer 1 pre-LLM mental-health chatbots and deployed systems, so the search needs to deliberately pick those up.

## Local sources you already have (use as seed + methods-transfer justification)

- Literature pack root: `/Users/ryangichuru/Documents/SSD-K/Uni/3rd year/NLP/Assignment 2/Literature Review`
- Seed list + links + priority tiers: `/Users/ryangichuru/Documents/SSD-K/Uni/3rd year/NLP/Assignment 2/Literature Review/sources/PRIORITY_READING_LIST.csv`
- Bucket summary + bibliography: `/Users/ryangichuru/Documents/SSD-K/Uni/3rd year/NLP/Assignment 2/Literature Review/README.md`
- Layer-2 folder organisation: `/Users/ryangichuru/Documents/SSD-K/Uni/3rd year/NLP/Assignment 2/Literature Review/sources/README.md`

## A. What you are building (so scope does not explode)

You are writing a PRISMA-ScR scoping review that functions as an evidence map for mental-health conversational AI / LLMs:

1. What systems exist (chatbots, conversational agents, LLM-based assistants) and what they are used for in mental health.
2. How they are evaluated (clinical outcomes, safety outcomes, technical outcomes; human vs automated; single-turn vs multi-turn).
3. What counts as “ground truth” / reference standard (clinician annotation, validated scales, guideline-scripted gold, synthetic vignettes).
4. Which reliability and safety gaps remain.

Your technical paper is the “answer” to the gaps you document: a benchmark/framework organised around:

- Study A: faithfulness (plus any “silent bias / empathy gap” evidence you can justify as part of evaluation reliability).
- Study B: sycophancy / user-pressure susceptibility.
- Study C: multi-turn drift / consistency.

Key design choice: two-layer evidence base.

- Layer 1 (primary): mental-health dialogue studies (therapy-style chat, screening, crisis, psychoeducation, clinician support).
- Layer 2 (methods-transfer): general conversational AI/LLM evaluation papers that define or operationalise sycophancy/pressure and drift/consistency tests (and faithfulness), even if not mental-health-specific.

If you cannot justify a measurement choice from Layer 1, you cite Layer 2 and explicitly say “this method has not yet been applied in mental-health dialogue evaluation”.

## B. Pick PCC and lock it

Use PCC (Population–Concept–Context). Write it once and reuse it everywhere (protocol, methods, inclusion criteria, extraction).

### Recommended PCC (tight but meaningful)

1. Population
- People receiving mental health support (or target clinical populations described in the study).
- Clinicians/health systems using conversational AI in mental health workflows.
- Studies evaluating mental-health conversational agents / LLMs.

2. Concept
- Reliability and safety evaluation of conversational AI/LLMs for mental health, with emphasis on:
  - Faithfulness of explanations/reasoning to outputs.
  - Susceptibility to user beliefs/persuasion/preference pressure (sycophancy).
  - Multi-turn consistency / longitudinal drift.
- Plus: ground-truth practices (clinician labels, validated instruments, synthetic vignettes, guideline scripts).

3. Context
- Mental health settings and tasks:
  - Screening/triage, therapy support, psychoeducation, crisis/risk handling, clinician support, documentation.
  - Single-turn and multi-turn dialogue.

## C. Objectives and RQs matching A/B/C (plus bias)

Primary questions (benchmark-aligned)

- RQ1 Faithfulness: How do mental-health conversational AI/LLM studies evaluate whether explanations or reasoning are aligned with (or causally support) the clinical output, and what proxies/metrics are used?
- RQ2 Sycophancy/pressure: How do conversational AI/LLM studies test and evaluate susceptibility to user beliefs, persuasion, or preference pressure in mental-health dialogue, and what harmful behaviours are measured?
- RQ3 Drift: How do conversational AI/LLM studies test and evaluate multi-turn consistency of patient state, safety constraints, and plan adherence over time (within-session or longitudinal), and what drift patterns are reported?

Secondary questions (clinician-facing)

- RQ4 Ground truth: What constitutes “ground truth” (clinician annotation, validated scales, scripted gold, synthetic labels), and what validity limitations are acknowledged?
- RQ5 Mitigations: What guardrails (prompting, fine-tuning, retrieval/memory, refusal policies, oversight) are tested and what evidence exists that they reduce harm?
- RQ6 Equity and empathy: Do studies evaluate bias, stigma, or differential empathy/quality across demographic groups, and how is it operationalised?

Objective statement template (pasteable)

> This PRISMA-ScR scoping review maps the landscape of conversational AI and LLM applications in mental health care, characterises evaluation methods and ground-truth practices, and identifies reliability and safety gaps related to faithfulness, susceptibility to user pressure, multi-turn consistency, and equity, to inform future benchmarking and safer deployment.

## D. Eligibility criteria (inclusion/exclusion) to prevent scope creep

Define criteria once, then enforce consistently in screening and extraction.

### D1) Inclusion (Layer 1: mental-health dialogue primary evidence)

Include studies that meet ALL of:

1. Conversational system (chatbot / conversational agent / LLM assistant), i.e. interactive dialogue, not just one-shot generation.
2. Mental health context or task (screening, therapy support, crisis, psychoeducation, clinician support, substance use services, etc.).
3. Contains evaluation data (quantitative, qualitative, mixed-methods, or structured rubric-based evaluation).

And at least ONE of:

- Reports clinical outcomes or validated instrument outcomes (e.g., symptom scales).
- Reports safety or harmful behaviour outcomes (incl. crisis handling, unsafe reassurance, boundary violations, misinformation, bias/stigma).
- Uses multi-turn protocols (or repeated interactions) with any consistency assessment.

### D2) Inclusion (Layer 2: methods-transfer evidence)

Include general conversational AI/LLM evaluation papers if they meet ALL of:

1. Propose or evaluate methods specifically relevant to RQ1/RQ2/RQ3 (faithfulness measures, pressure tests/sycophancy, multi-turn consistency/drift).
2. Transferable to mental-health dialogue evaluation (state “how” in extraction).
3. Contains an operational definition plus test protocol and/or scoring method (not purely opinion).

### D3) Exclusion

- Pure commentary/opinion without a described evaluation method.
- Non-conversational ML systems (unless explicitly a dialogue agent).
- General clinical LLM QA papers with no mental-health dialogue component and no transferable evaluation method.

### D4) Time window

Pick one and state it explicitly.

- LLM era (recommended): 2019–present.
- CA era (broader context): 2015–present.

If you choose 2015–present, pre-register (even informally) that you will not attempt outcome meta-analysis; you are mapping system types + evaluations.

## E. Search strategy (reproducible but realistic)

Goal: reproducible and transparent, not maximal.

### E1) Information sources (choose a feasible subset)

- PubMed/MEDLINE (clinical)
- JMIR (digital health and CA evaluations)
- IEEE Xplore / ACM Digital Library (technical CA methods)
- arXiv / medRxiv (recent LLM methods and evaluations)
- Optional if you have access: PsycINFO, Scopus/Web of Science.

### E2) Search string skeleton (adapt per database)

System terms:
- ("large language model" OR LLM OR "generative AI" OR chatbot OR "conversational agent" OR "dialogue system" OR "virtual therapist" OR "mental health assistant")

Mental-health terms:
- ("mental health" OR "behavio*ral health" OR psychiat* OR psycholog* OR depress* OR anxi* OR suicid* OR "self-harm" OR psychotherapy OR counselling OR counseling OR CBT OR "substance use" OR addiction)

Evaluation terms:
- (evaluation OR benchmark OR safety OR reliability OR hallucination OR bias OR stigma OR empathy OR "multi-turn" OR consistency OR drift OR longitudinal OR "user pressure" OR persuasion OR sycophan*)

Combine:
- (system) AND (mental-health) AND (evaluation)

### E3) Two-pass search (recommended)

- Pass 1 (Layer 1): mental-health constrained search.
- Pass 2 (Layer 2): loosen mental-health constraints but keep evaluation terms strong for faithfulness/pressure/drift.

### E4) Reproducibility requirements

Record and later report:

- Date searched
- Databases used
- Exact query strings (per database)
- Filters (year, language)
- Export format and dedup method

## F. Screening workflow (fast, defensible)

If solo, use a minimum viable workflow but make it auditable.

1. Deduplicate (record tool and strategy).
2. Title/abstract screen (single pass with a short checklist).
3. Full-text screen.
4. QC: re-screen a random 10–20% sample of excluded abstracts to estimate miss rate (report as limitation).

Title/abstract checklist:

- Is it a conversational agent/chatbot/LLM dialogue system (interactive dialogue)?
- Is mental health involved OR does it present a transferable evaluation method for faithfulness/pressure/drift?
- Does it include an evaluation (not just a proposal/opinion)?
- Does it mention outcomes, safety, pressure tests, multi-turn consistency, or evaluation metrics?

Full-text exclusion reasons (track explicitly):

- Not a conversational agent
- Not mental health and not methods-transfer
- No evaluation method/results
- Duplicate/secondary report of same evaluation (keep best/most complete)

## G. Data charting form (extraction template)

Treat the charting sheet as the dataset of the review. Use `docs/scoping_review/charting_template.csv` as the header.

Add these extra fields if you want your A/B/C positioning to read as inevitable (instead of hand-wavy):

- “User-pressure design realism” tag (low/medium/high): does the pressure mimic plausible mental-health user behaviour (insistence, reassurance seeking, self-diagnosis certainty, crisis manipulation)?
- “State tracked” tag (for drift): symptoms, risk status, safety constraints, care plan, medication facts, patient preferences.
- “Equity axis” tag: which groups were tested (race/ethnicity, gender, age, SES, etc.).

## H. Synthesis outputs (Results shape)

Think “map + taxonomy”, not meta-analysis.

Minimum outputs:

1. Evidence map: studies per year and per use-case.
2. Evaluation taxonomy table: human vs automated vs hybrid; single-turn vs multi-turn; ground-truth types.
3. Coverage matrix (A/B/C + bias): rows=studies; cols=faithfulness/pressure/drift/equity; plus ground truth type.
4. Harm taxonomy table: harms measured, how, and in which contexts.
5. Narrative: 5–8 key gaps tied to clinical risk.

## I. Where to introduce your benchmark in the scoping review

Do it in Discussion as a response to identified gaps, without leaking implementation detail.

Suggested subsection:

Discussion → “Implications for evaluation and safe deployment”

1. Faithfulness evaluation inconsistent / weak reference standards
2. User-pressure susceptibility under-tested in mental-health dialogues
3. Multi-turn drift and state consistency under-measured
4. Equity/empathy evaluation is sporadic or non-standardised
5. Proposed solution: benchmark organised around (A) faithfulness, (B) pressure, (C) drift, with explicit harm and equity reporting

## J. Local seed set (minimum viable citations to justify A/B/C choices)

These are already in your local priority list (`sources/PRIORITY_READING_LIST.csv`) and/or downloaded PDFs under `sources/**`.

Faithfulness (Layer 2)
- Lanham et al. (2023) Measuring faithfulness in chain-of-thought reasoning.
- Paul et al. (2024) Making reasoning matter (FRODO / causal framing).
- Turpin et al. (2023) Language models do not always say what they think (unfaithful rationales).

User pressure / sycophancy (Layer 2)
- Wei et al. (2023) Simple synthetic data reduces sycophancy (RLHF effects + mitigation).
- Anthropic (2024) Towards understanding sycophancy (definitions + behaviours).
- Fanous et al. (2025) SycEval (eval protocol; labelled as “clinical context” in your list).
- Kaur (2025) Echoes of agreement (argument-driven pressure sequences).
- Pandey et al. (2025) Beacon (latent sycophancy diagnostics).
- Hong et al. (2025) ELEPHANT / SYCON-Bench (social framing effects).
- Liu et al. (2025) Truth decay (multi-turn sycophancy).

Drift / multi-turn consistency (Layer 2)
- Laban et al. (2025) Multi-turn degradation (“gets lost”).
- Zheng et al. (2024) Why LLMs fail in multi-turn conversations (analysis + fixes).
- Kruse et al. (2025) Temporal reasoning for longitudinal clinical summarisation (methods you can adapt).

Mental-health domain anchors (Layer 1/bridge)
- Zhang et al. (2025) PsyLLM / “Beyond empathy” (mental health counselling reasoning pipeline).
- Gabriel et al. (2024) “Can AI relate” (empathy gap / race inference and differential responses).

## K. Known missing (what to add to the local evidence base)

Right now, the local pack is rich for Layer 2 and “clinical LLM” methods. It is thin for Layer 1 studies that evaluate actual mental-health conversational agents (including pre-LLM chatbots) with outcomes, usability, and safety handling.

Actionable fix: bias Pass 1 search to deliberately surface those studies (JMIR + PubMed), then backfill your charting sheet.

## L. Reporting checklist and exemplars (optional, but saves time)

Reporting standard
- PRISMA-ScR checklist + explanation: https://pubmed.ncbi.nlm.nih.gov/30178033/
- PRISMA scoping reviews: https://www.prisma-statement.org/scoping
- EQUATOR PRISMA-ScR page: https://www.equator-network.org/reporting-guidelines/prisma-scr/

Recent mental-health LLM / conversational AI scoping reviews (as writing exemplars)
- npj Digital Medicine (2025) scoping review of LLMs in mental health care: https://www.nature.com/articles/s41746-025-01611-4
- JMIR (2025) applications of LLMs in mental health: https://www.jmir.org/2025/1/e69284
- JMIR (2023) evaluating conversational agents for mental health: https://www.jmir.org/2023/1/e44548/
