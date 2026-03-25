# TPEA Paper Literature Verification & Paper Update Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Verify all literature claims in paper.tex against primary sources, identify gaps in HE/education-specific references, and update the paper with defensible, correctly cited content.

**Architecture:** Three-phase approach: (1) parallel research subagents verify existing citations and search for missing HE references, (2) sequential paper edits integrate verified claims and new citations, (3) final consistency check across all sections.

**Tech Stack:** Research subagents for web verification, Edit tool for paper.tex updates, Harvard referencing (natbib authoryear).

---

## Phase 1: Literature Verification (Parallel Research Subagents)

### Task 1: Verify Existing Citations — Sycophancy Cluster

**Files:**
- Read: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 93-175)
- Read: `Assignment 2/Literature Review/README.md` (items 12-29)
- Read: `Assignment 2/Literature Review/sources/PRIORITY_READING_LIST.csv` (rows 12-29)

**Step 1: Dispatch research subagent to verify sycophancy citations**

Verify these three papers and the specific claims made about them in paper.tex:

| Citation Key | Claim in paper.tex | Verify |
|---|---|---|
| `wei2023sycophancy` | "LLMs exhibit sycophantic behaviour—agreeing with users even when factually wrong" (line 94-95); "RLHF can induce this behaviour" (line 172) | Confirm Wei et al. 2023 supports both claims. Check: is "RLHF increases sycophancy from ~18% to 75%" (from README) the correct figure? |
| `sharma2024sycophancy` | Co-cited with Wei for same sycophancy claim (line 95) | Confirm Sharma et al. 2024 (arXiv:2310.13548) supports the claim. Note: README lists this as "Anthropic (2024)" — verify authorship. |
| `liu2025truth` | "truth decay... degrade significantly as repeatedly challenged in multi-turn" (line 191-193); "Multi-turn dialogue systems lose track of critical context" (line 96-97) | Confirm Liu et al. 2025 (arXiv:2503.11656) supports both claims. Check: does it report the "up to 47% accuracy drops" figure from the assignment? |

Also check whether **Fanous et al. (2025) SycEval** (arXiv:2502.08177) and **Lee et al. (2025) "When Helpfulness Backfires"** from the priority list are worth citing for the clinical sycophancy angle — they are Tier 1/2.

**Expected output:** Per-citation verification (CONFIRMED / NEEDS CORRECTION / NEEDS NUANCE) with exact quotes or page numbers from primary sources.

---

### Task 2: Verify Existing Citations — Faithfulness & Bias Cluster

**Files:**
- Read: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 144-212)
- Read: `Assignment 2/Literature Review/README.md` (items 1-11, 38-42)

**Step 1: Dispatch research subagent to verify faithfulness/bias citations**

| Citation Key | Claim in paper.tex | Verify |
|---|---|---|
| `turpin2023lmdont` | Figure 1 caption: "unfaithful reasoning" (line 148) | Confirm Turpin et al. 2023 (NeurIPS) demonstrates unfaithful CoT. Check: "36% accuracy drop with biasing features" figure from README — is this from Turpin? |
| `lanham2024reasoning` | Figure 1 caption: co-cited for "unfaithful reasoning" (line 148) | Confirm Lanham et al. 2024 (arXiv:2402.13950) is the faithfulness gap paper. Note: README says "arXiv:2307.13702" for the 2023 version — is the 2024 version correct? |
| `hu2025psyllm` | "domain-specific fine-tuning does not necessarily resolve the issue" (line 210) | Confirm Hu et al. 2025 supports this claim. Check: the paper is about PsyLLM; does it actually show fine-tuning doesn't fix bias, or does it claim the opposite? This is a critical claim to get right. |
| `stadia2024can` | "models attempting empathy often over-agree with users in ways that can reinforce harmful patterns" (line 208-209) | Confirm Stadia/Gabriel et al. 2024 (EMNLP Findings) supports this. Check: README lists "2-13% lower empathy for Black patients" — is "over-agreeing" the right characterisation? |
| `singhal2023expert` | "MedQA demonstrate impressive headline performance" (line 105) | Confirm Singhal et al. 2023 (Nature) is the correct Med-PaLM paper. |
| `he2025survey` | "metrics mask profound fragilities in reasoning reliability" (line 107-108); "Bias in LLM outputs... differential treatment" (line 98) | Confirm He et al. 2025 (Information Fusion) supports both claims. |

Also check whether **Hager et al. (2024)** "Evaluation and Mitigation of the Limitations of LLMs in Clinical Decision-Making" (Nature Medicine, Tier 1) should be cited — the README says "Models fail in realistic workflows despite expert-level exam scores" which directly supports the paper's argument.

**Expected output:** Per-citation verification with exact quotes/findings.

---

### Task 3: Search for Missing HE/Education-Specific References

**Files:**
- Read: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 613-617, the PLACEHOLDER comment)
- Read: `Assignment 2/Literature Review/misc/Notes/Notes 2.txt` (mental health clinical review notes)

**Step 1: Dispatch research subagent to find HE AI deployment literature**

The paper.tex has a `% PLACEHOLDER` at line 613 requesting:
- HE AI adoption surveys
- Student mental health / counselling demand literature
- Institutional AI governance frameworks
- UK QAA / OfS guidance on AI in education

Search for and verify (2-4 papers max — this is a 3000-word paper):

1. **UK HE student mental health demand** — a recent survey/report showing increasing demand on counselling services (to justify the "overstretched counselling services" claim in the Introduction, line 83). Possible sources: UUK Student Mental Health report, Student Minds, IPPR.

2. **HE institutions adopting AI chatbots** — any recent report or case study of UK universities piloting AI wellbeing tools (to justify "being considered for roles ranging from mental health triage" claim, line 81-82). Check Russell Group digital strategy, Jisc reports, or HEPI.

3. **UK institutional AI governance** — QAA/OfS/Jisc guidance on responsible AI use in HE (to support Section 5 "Institutional Considerations"). Check if QAA has published AI guidance in 2024-2025.

4. **Laban et al. (2025)** "LLMs Get Lost In Multi-Turn Conversation" (arXiv:2505.06120) — already in the priority list as Tier 1. Verify the "39% average degradation" claim and determine if it should be cited alongside Liu et al. for drift evidence.

**Expected output:** 2-4 verified references with Harvard-format citation entries, key findings, and where they should be cited in paper.tex.

---

## Phase 2: Paper Updates (Sequential)

### Task 4: Update References Section

**Files:**
- Modify: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 547-618)

**Step 1: Add verified new references**

Based on Task 1-3 outputs, add new `\bibitem` entries in Harvard format for:
- Any new HE/education references from Task 3
- Hager et al. (2024) if confirmed relevant
- Laban et al. (2025) if confirmed relevant
- Any additional sycophancy/clinical sources from Task 1 if needed

Each entry must follow the existing format:
```latex
\bibitem[Author et~al., Year]{citekey}
Author, A., Author, B. and Author, C. (Year) `Title of article',
\textit{Journal Name}, Volume(Issue), pp.~Pages.
doi:~\href{https://doi.org/...}{10.xxxx/...}.
```

**Step 2: Remove the PLACEHOLDER comment at line 613**

Replace with the actual entries.

**Step 3: Verify no orphan citations**

Check every `\citep{}` and `\citet{}` in the document has a matching `\bibitem`.

---

### Task 5: Update Section 1 (Introduction) with HE References

**Files:**
- Modify: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 75-131)

**Step 1: Add HE deployment citation**

Line 81-83 currently reads:
```
Large language models, deployed as conversational agents, are being considered
for roles ranging from mental health triage to ongoing wellbeing check-ins.
```
Add a citation from Task 3 results (HE AI adoption report).

**Step 2: Add student demand citation**

Line 83 currently reads:
```
scalable, always-available support that can supplement overstretched
counselling services.
```
Add a citation from Task 3 results (UK student mental health demand report).

**Step 3: Add Hager citation if confirmed**

If Hager et al. (2024) is confirmed, add to line 105-110 alongside the existing He et al. citation to strengthen the "static benchmarks mask fragilities" argument.

---

### Task 6: Update Section 2 (Failure Modes) with Verified Claims

**Files:**
- Modify: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 134-212)

**Step 1: Correct any claims flagged by Tasks 1-2**

If any citation verification returned "NEEDS CORRECTION" or "NEEDS NUANCE", update the relevant sentences in Sections 2.1, 2.2, 2.3.

**Step 2: Add Laban et al. citation if confirmed**

If Laban et al. (2025) is confirmed relevant, add to Section 2.2 (Multi-Turn Memory Drift) alongside the existing Liu et al. citation. The "39% degradation" figure is strong supporting evidence.

**Step 3: Verify Stadia/Gabriel authorship**

The README lists this as "Gabriel et al." (item 41) but paper.tex uses `stadia2024can`. Confirm correct first author and update the `\bibitem` if needed.

---

### Task 7: Update Section 5 (Implications) with Governance Reference

**Files:**
- Modify: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (lines 482-497)

**Step 1: Add institutional governance citation**

If a QAA/OfS/Jisc reference was found in Task 3, add it to the "Institutional Considerations" subsection (line 487-497) to support the claim that institutions should require failure-mode testing.

---

## Phase 3: Final Verification

### Task 8: Cross-Check All Claims Against Sources

**Files:**
- Read: `Assignment 2/papers/00a-tpea-advancing-education/paper.tex` (full file)

**Step 1: List every factual claim in the paper**

Extract every sentence that makes a factual claim (not the authors' own contribution/findings).

**Step 2: Check each claim has a citation**

Unsupported factual claims must either gain a citation or be reworded as the authors' observation.

**Step 3: Check no citation is overclaimed**

No paper should be cited for a claim stronger than what it actually demonstrates.

**Step 4: Run through source-grounding checklist**

- [ ] Every factual claim has at least one citation
- [ ] No citation is used for a claim the source doesn't support
- [ ] Harvard format consistent (Author, Year) throughout
- [ ] No `\cite{}` used — all converted to `\citep{}` or `\citet{}`
- [ ] Reference list alphabetical by first author surname
- [ ] No orphan references (every `\bibitem` cited at least once)
- [ ] No orphan citations (every `\citep/\citet` has a `\bibitem`)

---

### Task 9: Commit Verified Paper

**Step 1: Stage the updated paper.tex**

```bash
git add "Assignment 2/papers/00a-tpea-advancing-education/paper.tex"
```

**Step 2: Commit**

```bash
git commit -m "docs(tpea-paper): verify literature claims and add HE-specific references

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>"
```

---

## Reference: Claims-to-Verify Matrix

| Line(s) | Claim | Current Citation | Status |
|----------|-------|-----------------|--------|
| 81-82 | LLMs considered for mental health triage in HE | NONE | Needs HE ref |
| 83 | Overstretched counselling services | NONE | Needs demand ref |
| 94-95 | LLMs exhibit sycophantic behaviour | Wei 2023, Sharma 2024 | Verify |
| 96-97 | Multi-turn systems lose critical context | Liu 2025 | Verify |
| 98-99 | Bias/differential treatment persistent | He 2025 | Verify |
| 105-106 | MedQA impressive headline performance | Singhal 2023 | Verify |
| 107-108 | Metrics mask fragilities in reasoning | He 2025 | Verify |
| 148 | Unfaithful reasoning | Turpin 2023, Lanham 2024 | Verify |
| 150 | Contextual drift | Liu 2025 | Verify |
| 168-169 | Capitulation difficult to detect | Liu 2025 | Verify |
| 172-174 | RLHF induces sycophancy | Wei 2023 | Verify |
| 189-190 | No persistent memory beyond context window | — | Common knowledge, OK |
| 191-193 | Truth decay degrades significantly | Liu 2025 | Verify |
| 208-209 | Models over-agree when attempting empathy | Stadia 2024 | Verify |
| 210 | Domain fine-tuning doesn't resolve bias | Hu 2025 | Verify — critical |
| 487 | Institutions should require failure-mode testing | NONE | Needs governance ref |
