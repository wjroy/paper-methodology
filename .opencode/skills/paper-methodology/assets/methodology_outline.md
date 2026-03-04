# Methodology Section Outline

> Flexible hierarchy template extracted from 9 reference papers in the geotechnical AI domain.
> This is a **guideline**, not a rigid template. Adapt section ordering and depth to the specific paper.

## General Narrative Flow (Invariant Pattern)

Every methodology section follows this macro-structure:

1. **Opening Overview Paragraph** (~100-200 words)
   - One paragraph that summarizes the entire methodology
   - Lists 3-5 numbered high-level steps
   - Names the key components/modules
   - Example pattern: "The proposed framework consists of three main components: (1) ..., (2) ..., and (3) ..."

2. **Detailed Subsections** (one per major component)
   - Each numbered step from the overview becomes a subsection
   - Each subsection opens with a brief motivation sentence before technical detail
   - Subsections may contain sub-subsections for complex components

3. **Closing Integration** (optional)
   - Loss function / objective formulation
   - Training procedure summary
   - Evaluation metrics definition

---

## Typical Section Hierarchy

```
X. Methodology / Methods
   X.1 Overall Framework / Problem Formulation
       - Overview paragraph with numbered steps
       - Figure reference: "as shown in Figure X"
       - Optional: notation table (Table 1)

   X.2 Physical / Mechanical Modeling (if applicable)
       - Analytical model derivation
       - Governing equations
       - Assumptions and boundary conditions
       - "Where ..." variable definition blocks

   X.3 Data Generation / Processing
       - Data source description
       - Simulation setup (if synthetic data)
       - Feature engineering / input-output definition
       - Normalization / preprocessing steps
       - Train-validation-test split rationale

   X.4 Model Architecture
       X.4.1 Component A (e.g., encoder, graph module)
       X.4.2 Component B (e.g., temporal module, attention)
       X.4.3 Component C (e.g., decoder, generator)
       - Each sub-subsection: motivation -> formulation -> equation -> variable definitions

   X.5 Loss Function / Training Strategy
       - Loss function formulation
       - Optimization algorithm and hyperparameters
       - Training procedure (epochs, early stopping, etc.)

   X.6 Evaluation Metrics (sometimes in Experiments)
       - Metric definitions with equations
       - Justification for metric choice
```

---

## Pattern Variations by Paper Type

### Surrogate Model Papers (e.g., PitGAN, Two-stage SVM)
- Physics model comes first, then data generation, then ML architecture
- Emphasis on how physics informs the surrogate

### Spatiotemporal Prediction Papers (e.g., PI-ETGCN, AC-GGN, MS-STGCN)
- Graph construction method is a dedicated subsection
- Spatial and temporal modules are separate sub-subsections
- Adjacency matrix definition is critical

### LLM-Enhanced Papers (e.g., LLM-GNN, LLM-KG)
- LLM integration point is a dedicated subsection
- Prompt design / ICL strategy described in detail
- Embedding extraction pipeline explained

### Risk Assessment Papers (e.g., TSFRA)
- Indicator system construction comes first
- Weight determination method (AHP, entropy, etc.)
- Risk grade classification criteria

---

## Section Opening Patterns (from reference papers)

Use these as natural paragraph starters (not a checklist):

- "The overall framework of the proposed [METHOD] is illustrated in Figure X."
- "To address the challenge of [PROBLEM], this study proposes [METHOD]."
- "The proposed methodology comprises three main stages: ..."
- "In this section, the detailed architecture of [METHOD] is presented."
- "To be more specific, the [COMPONENT] module is designed to ..."
- "The mathematical formulation is detailed as follows."
- "As illustrated in Fig. X, the [MODULE] takes [INPUT] and produces [OUTPUT]."

---

## Equation-Prose Integration Pattern

Every equation block follows this sequence:

```
[Motivation sentence explaining WHY this equation is needed]

[Equation (N)]

where [symbol_1] denotes [definition], [symbol_2] represents [definition], ...
[Optional: interpretation sentence explaining WHAT the equation means physically]
```

Example:
"The lateral displacement of the retaining wall can be computed as:

[Equation (3)]

where delta_w denotes the wall displacement at depth z, E_s represents the soil elastic modulus, and H is the excavation depth. This formulation captures the coupling between soil stiffness and excavation geometry."
