# Error Log — Persistent Correction Memory

> This file records user corrections from past sessions. The AI MUST read this
> file before every text generation and avoid repeating any logged mistake.
>
> Format: Each entry is a correction the user made. The AI should treat these
> as "negative constraints" — things that must NOT appear in future output.
>
> Maintenance: The AI appends new entries when the user corrects its output.
> Entries are never deleted (they accumulate as learning).

---

## How to Use This File

### Before Generation (AI reads)
1. Read all entries below.
2. For each entry, internalize the correction as a rule.
3. During drafting, actively check against these rules.
4. If uncertain whether a pattern matches a logged error, err on the side of
   following the correction.

### After User Correction (AI writes)
When the user corrects your output, append a new entry using this format:

```
### [CATEGORY] — Brief Description
- Date: YYYY-MM-DD
- Wrong: [what the AI produced]
- Correct: [what the user wanted]
- Context: [which section/paper this occurred in]
- Rule: [the general rule to prevent recurrence]
```

### Categories
- TERMINOLOGY: wrong term choice or inconsistent term usage
- FORMATTING: punctuation, spacing, Markdown leaks, structure issues
- STYLE: tone, voice, register, or vocabulary problems
- FACTUAL: incorrect technical claims or fabricated values
- STRUCTURAL: wrong section ordering, missing sections, alignment issues
- TRANSLATION: CN-EN mismatch, mistranslation, or inconsistent rendering

---

## Error Entries

### FACTUAL — THGAN application domain misidentified as tunnel instead of pit
- Date: 2026-03-05
- Wrong: "THGAN is for tunnel health monitoring"
- Correct: "THGAN is for deep excavation (pit) risk prediction using digital twin"
- Context: reference_papers/README.md, Line 24; also affects any auto-generated summaries
- Rule: Always verify application domain from the paper content itself, not from model name or abstract keywords. THGAN explicitly focuses on "deep excavation", "retaining wall deflection", "ground settlement", and "excavation unloading" — all characteristic of pit excavation, NOT tunneling. No mention of "tunnel", "shield", or "TBM" anywhere in the paper.
- Evidence: 03-own-THGAN.txt mentions "deep excavation" (L12, L54), "retaining wall" (L16, L54), "excavation-side soil" (L16), "pit excavation" (implicit throughout IBS model), and typical pit monitoring (wall deflection + ground settlement). Zero tunnel-related terms.

### TERMINOLOGY — LTSM ≠ LSTM
- Date: 2026-03-06
- Wrong: "LSTM (Large Time Series Model)" or treating LTSM as a typo for LSTM
- Correct: "LTSM = Large Time Series Model (e.g., Timer); LSTM = Long Short-Term Memory (RNN variant)"
- Context: reference_papers/15-other-Wind-FM.txt uses "LTSM" throughout
- Rule: When referencing Paper 15 (Wind-FM), always expand LTSM as "Large Time Series Model". Never auto-correct to LSTM. These are completely different concepts — LTSM refers to foundation models for time series (like Timer), while LSTM is a specific RNN architecture.

### TERMINOLOGY — Cloud Model is mathematical, not cloud computing
- Date: 2026-03-06
- Wrong: Interpreting "Cloud Model" as cloud computing or cloud-based architecture
- Correct: "Cloud Model" is a mathematical uncertainty model with parameters Ex (expected value), En (entropy), He (hyper-entropy)
- Context: reference_papers/12-other-CM-risk.txt; hard_memory.json key "云模型"
- Rule: When referencing Paper 12 or the term "Cloud Model", always clarify it is a probability-to-fuzzy conversion model for uncertainty quantification. It has nothing to do with cloud computing infrastructure.

### TERMINOLOGY — MS in MS-STGCN = Multi-Source, not Multi-Scale
- Date: 2026-03-06
- Wrong: "Multi-Scale Spatiotemporal Graph Convolutional Network"
- Correct: "Multi-Source Spatiotemporal Graph Convolutional Network"
- Context: reference_papers/09-other-MS-STGCN.txt
- Rule: MS-STGCN fuses multi-source monitoring data (inclinometers, settlement gauges, etc.), not multi-scale features. Always expand "MS" as "Multi-Source" when referencing this paper.

### STYLE — Overusing first-person "we" in English Methods
- Date: 2026-03-06
- Wrong: Setting Methods voice as moderate first-person usage (e.g., "we propose", "we design")
- Correct: Use rare-to-none first-person in Methods; prefer "this study", "this paper", or "the proposed framework"
- Context: own papers 01-05 methodology sections
- Rule: Do not enforce "we" usage in Methods. Treat first-person as rare-to-none unless user explicitly requests otherwise.

### STRUCTURAL — Forcing physics-first as invariant order
- Date: 2026-03-06
- Wrong: "Physics/mechanics always precedes architecture for all own papers"
- Correct: Select a pattern from methodology_patterns.yml; use base skeleton + overlay
- Context: own papers 04 (LLM-GNN) and 05 (TSFRA) do not follow physics-first structure
- Rule: Never claim a universal invariant section order across all own papers.

### TERMINOLOGY — Locking context-dependent CN terms to a single EN variant
- Date: 2026-03-06
- Wrong: Hard-locking 基坑 to one EN variant and rejecting alternatives
- Correct: Use context-dependent variants (deep excavation / excavation / foundation pit / excavation pit)
- Context: own papers 01-05 use multiple valid variants
- Rule: For context-dependent terms, enforce "no mistranslation" instead of single-variant lock.

### STRUCTURAL — Generalizing global style rules from partial own-paper samples
- Date: 2026-03-06
- Wrong: Calibrating style/pattern/logic rules from only 2-3 own papers
- Correct: Rule-refinement must use all own papers 01-05; runtime generation may retrieve only top 2-3 relevant papers for efficiency
- Context: skill maintenance and pattern/style updates
- Rule: Separate calibration scope from runtime scope. Full own-paper coverage is required for rule updates; selective retrieval is runtime-only.
