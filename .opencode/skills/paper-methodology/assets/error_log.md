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

### TERMINOLOGY — "excavation pit" never appears in own papers
- Date: 2026-03-06
- Wrong: Rendering 基坑 as "excavation pit" in hard_memory and glossary
- Correct: Use "deep excavation" or "excavation" (Papers 02-04), or "foundation pit" (Papers 01, 05). The term "excavation pit" was not found in any of the 5 own papers.
- Context: hard_memory.json, term_glossary.yml — previously set "excavation pit" as the sole mapping for 基坑
- Rule: 基坑 is context-dependent. Check the target paper's convention. Default to "deep excavation" for geotechnical-AI contexts.

### STYLE — First-person "we/our/us" never used in own papers
- Date: 2026-03-06
- Wrong: soft_memory and style_profile claimed "moderate, 5-10 instances of 'we'" and listed preferred phrases like "We design", "We propose"
- Correct: All 5 own papers use ZERO first-person pronouns. The self-reference is "this study" (4/5 papers) or "this paper" (Paper 01).
- Context: soft_memory.json voice_preferences, style_profile.md §3
- Rule: Never generate "we/our/us" in methodology output unless the user explicitly requests it. Always use "this study" or passive voice.

### STYLE — "physics-first invariant" was overstated
- Date: 2026-03-06
- Wrong: soft_memory claimed "Physics model always precedes neural architecture. This is the invariant pattern across the own paper set."
- Correct: Physics/mechanics precedes architecture in 3/5 papers (01, 02, 03). Papers 04 and 05 have no physics module. The actual invariant is: framework overview first, then module-by-module in pipeline order.
- Context: soft_memory.json section_ordering_preference, style_profile.md §1
- Rule: Do not force a physics section into methodology when the user's method has no physics/mechanics component.

### TERMINOLOGY — "ground surface settlement" full form never used
- Date: 2026-03-06
- Wrong: hard_memory mapped 地表沉降 to "ground surface settlement"
- Correct: Own papers consistently use "ground settlement" (without "surface")
- Context: hard_memory.json, term_glossary.yml
- Rule: Default to "ground settlement" for 地表沉降.

<!-- 
Example entries removed — superseded by real entries above.
-->### FORMATTING — Markdown bold leaked into plain text output
- Date: 2025-01-16
- Wrong: "The **proposed framework** consists of..."
- Correct: "The proposed framework consists of..."
- Context: English methodology, Section 3.1
- Rule: Output must be plain text. No Markdown formatting (bold, italic, headings, bullets).
-->
