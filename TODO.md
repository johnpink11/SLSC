# SLSC Paper TODO List

## Missing Figures

### 1. Figure: fig:comparison (Introduction)
**Location:** `sections/introduction.tex`, line 53  
**Status:** ✅ Already exists in the paper (inline mdframed boxes)  
**Description:** Comparison of Natural-Language Summary vs. SLSC representation at Turn 3

### 2. Figure: fig:pipeline (Method)
**Location:** `sections/method.tex`, line 5  
**Status:** ❌ MISSING - Referenced but not created  
**Description:** Overall architecture diagram showing the SLSC framework
**Requirements:**
- Show the two-phase operation per turn: Reasoning (Agent A) and Curation (Agent B)
- Illustrate the flow: Problem P → Agent A (with S_{t-1}, q_t) → response r_t → Agent B → updated state S_t
- Visual representation of the twin-agent architecture
- Should be a flowchart or system diagram
**Suggested tool:** Draw.io, TikZ, or similar

### 3. Figure: fig:state_growth (Experiments)
**Location:** `sections/experiments.tex`, line 165  
**Status:** ✅ COMPLETED - Figure added with state_growth.png  
**Description:** Cumulative input tokens seen by Agent A as a function of turn index

### 4. Figure: fig:case_4b (Experiments)
**Location:** `sections/experiments.tex`, line 210  
**Status:** ✅ COMPLETED - Side-by-side comparison created  
**Description:** Representative 4B failure case showing Full History vs. SLSC (number_theory/1002)

### 5. Figure: fig:per_turn (Experiments)
**Location:** `sections/experiments.tex`, line 349  
**Status:** ✅ COMPLETED - Figure added with per_turn_by_mode.png  
**Description:** Per-turn Correct Turn Rate at Qwen3.5-4B scale

---

## Missing Tables (Data to Fill)

### 1. Table: tab:lean_quality (Experiments)
**Location:** `sections/experiments.tex`, line 112  
**Status:** ✅ COMPLETED - Data filled from manual annotation  
**Description:** Manual quality analysis of 50 randomly sampled Lean~4 outputs

### 2. Table: tab:fh_failure (Experiments)
**Location:** `sections/experiments.tex`, line 187  
**Status:** ✅ COMPLETED - Data filled from manual annotation (31 problems)  
**Description:** Failure mode distribution of Full History on Qwen3.5-4B

### 3. Table: tab:slsc_failure (Experiments)
**Location:** `sections/experiments.tex`, line 324  
**Status:** ✅ COMPLETED - Data filled from manual annotation (16 problems)  
**Description:** Failure mode distribution of compression methods on Qwen3.5-2B

---

## Missing Appendix Content

### 1. Appendix: app:dataset
**Location:** Referenced in `sections/experiments.tex`, line 5  
**Status:** ❌ MISSING - Referenced but not created  
**Description:** Dataset construction pipeline for Math-100-multi
**Content needed:**
- Detailed description of automated decomposition pipeline
- How single-turn MATH-500 problems are converted to multi-turn format
- Sub-question generation methodology
- Quality control and validation procedures
- Examples of original vs. decomposed problems
- Statistics on decomposition (avg turns, dependency types, etc.)

### 2. Appendix: app:prompts
**Location:** Referenced in `sections/method.tex` (line 69) and `sections/experiments.tex` (line 30)  
**Status:** ❌ MISSING - Referenced but not created  
**Description:** Full prompt templates for all agents
**Content needed:**
- Agent A (Reasoner) prompt template
- Agent B (Curator) prompt templates:
  - Extraction prompt
  - Merging prompt (with deduplication/supersession/preservation rules)
  - Formalization prompt (for Lean~4 augmentation)
- Summary baseline prompt
- All system messages and few-shot examples if used
- Sampling parameters (temperature, top-p, max_tokens, etc.)

### 3. Appendix: Implementation Details
**Location:** Referenced in `sections/experiments.tex`, line 66-68  
**Status:** ⚠️ INCOMPLETE - Placeholder text exists  
**Content needed:**
- GPU model specification (currently marked as [GPU model, e.g., 2× A100 80GB])
- Total inference time (currently marked as [XX hours])
- Code release information
- vLLM version and configuration
- Reproducibility details

---

## Missing Example Cases

### 1. Full Multi-Turn Problem Example
**Purpose:** Help readers understand the task setup  
**Content needed:**
- One complete Math-100-multi problem showing:
  - Original MATH-500 problem
  - Decomposed sub-questions (q₁, q₂, q₃, ...)
  - How each sub-question depends on previous numerical results
  - Expected answers for each turn
**Suggested location:** Early in experiments section or in appendix

### 2. Agent B Curation Example (Step-by-step)
**Purpose:** Illustrate the extraction → formalization → merging pipeline  
**Content needed:**
- Input: Agent A's response r_t
- Step 1: Extracted propositions P_t
- Step 2 (optional): Formalized Lean~4 stubs
- Step 3: Merged state S_t showing deduplication/supersession
**Note:** Partial example exists in method section (lines 42-57), but could be expanded

### 3. Failure Case Examples
**Purpose:** Illustrate the failure modes described in analysis  
**Content needed:**
- **Response-style cascade example:** Show how Full History induces verbose meta-reasoning
- **2B parsing failure example:** Show how 2B model ignores compressed state
- **Lean formalization error example:** Show hallucinated symbols or incorrect types

---

## Statistical Significance Testing

### Current Status
- McNemar's test p-values are reported in Table tab:main
- All comparisons are against "No Compression" baseline
- Significance markers: †(p<0.1), *(p<0.05), **(p<0.01), ***(p<0.001)

### Verification Needed
- ✅ Confirm all p-values in tab:main are computed correctly
- ⚠️ Consider adding pairwise comparisons between compression methods (Summary vs. SLSC)
- ⚠️ Consider reporting effect sizes (not just p-values) for better interpretation

---

## Code and Data Release

### Requirements (mentioned in paper)
**Location:** `sections/experiments.tex`, line 68  
**Status:** ⚠️ TODO  
**Items to release:**
- [ ] Math-100-multi dataset (100 problems with decompositions)
- [ ] Dataset construction scripts (automated decomposition pipeline)
- [ ] SLSC implementation code (Agent A, Agent B, inference pipeline)
- [ ] Evaluation scripts (answer normalization, metrics computation)
- [ ] All prompt templates (see app:prompts above)
- [ ] Experimental results (raw outputs, per-problem predictions)
- [ ] Reproduction instructions (environment setup, model serving, etc.)

**Suggested platform:** GitHub repository with clear README

---

## Writing Polish

### Minor Issues to Address

1. **Spelling/Grammar (from diagnostics):**
   - Line 8 (Conclusion): "autoformalization" flagged - verify if this is standard terminology
   - Line 13 (Conclusion): "testbed" flagged - consider "test bed" (two words)
   - Lines 196-237 (Experiments): Multiple "repeated word" warnings - review for typos

2. **Missing References:**
   - `fig:state_growth` (line 171) - commented out, needs to be created
   - `fig:per_turn` (line 248) - commented out, needs to be created

3. **LaTeX Warnings:**
   - Overfull hbox warnings (lines 230, etc.) - check table/text formatting
   - Underfull vbox warning (line 1) - likely harmless but review

---

## Priority Ranking

### High Priority (Required for submission)
1. ✅ Abstract - COMPLETED
2. ✅ Conclusion - COMPLETED
3. ❌ **Figure: fig:pipeline** - Core architecture diagram
4. ❌ **Appendix: app:prompts** - Essential for reproducibility
5. ❌ **Appendix: app:dataset** - Essential for understanding task
6. ✅ **Fill missing table data** - COMPLETED (tab:lean_quality, tab:fh_failure, tab:slsc_failure)

### Medium Priority (Strongly recommended)
7. ✅ **Figure: fig:state_growth** - COMPLETED
8. ✅ **Figure: fig:per_turn** - COMPLETED
9. ✅ **Figure: fig:case_4b** - COMPLETED
10. ⚠️ **Implementation details** - GPU specs, timing, code release plan

### Low Priority (Nice to have)
11. Additional example cases in appendix
12. Pairwise statistical comparisons between compression methods
13. Extended related work discussion

---

## Estimated Work Required

| Task | Estimated Time | Difficulty |
|------|---------------|------------|
| Create fig:pipeline | 2-3 hours | Medium |
| ~~Create fig:state_growth~~ | ~~1-2 hours~~ | ✅ DONE |
| ~~Create fig:per_turn~~ | ~~1-2 hours~~ | ✅ DONE |
| ~~Create fig:case_4b~~ | ~~2-3 hours~~ | ✅ DONE |
| Write app:prompts | 2-3 hours | Easy |
| Write app:dataset | 3-4 hours | Medium |
| ~~Annotate 50 Lean outputs~~ | ~~3-4 hours~~ | ✅ DONE |
| ~~Annotate 31 FH failures~~ | ~~2-3 hours~~ | ✅ DONE |
| ~~Annotate 16 2B failures~~ | ~~2-3 hours~~ | ✅ DONE |
| Fill implementation details | 0.5 hours | Easy |
| Code/data release prep | 4-6 hours | Medium |

**Total estimated time remaining:** 12-18.5 hours (down from 23-33 hours)

---

## Notes

- All figure references use `\ref{fig:...}` - ensure labels match
- All table references use `\ref{tab:...}` - ensure labels match
- All appendix references use `\ref{app:...}` - ensure labels match
- The paper uses EMNLP 2025 LaTeX template
- Current diagnostic shows the paper compiles but with warnings
- Token efficiency table (tab:tokens) has been fixed for double-column format
