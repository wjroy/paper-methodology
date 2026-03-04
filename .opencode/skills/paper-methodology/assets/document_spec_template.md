# Document Spec Template — MethodSpec with Definition of Done

> This template defines the MethodSpec structure used in Phase 3 (PLAN) of the
> workflow. Each section has a Definition of Done (DoD) — a checklist of concrete
> criteria that must be satisfied before the section is considered complete.
>
> The AI generates the MethodSpec by filling in this template. Before proceeding
> to the DRAFT step, every DoD must be met or the gap must be explicitly flagged
> as [TBD] in the TODO/VERIFY list.

---

## Revision Plan Protocol

> IMPORTANT: When the user requests a large modification to an already-generated
> output (changing section structure, adding/removing components, altering the
> framework), the AI MUST produce a Revision Plan BEFORE making changes.

### When a Revision Plan is Required
- Adding or removing a MethodSpec section
- Changing the framework's number of stages/components
- Modifying 3+ paragraphs in the methodology text
- Changing equation numbering or adding/removing equations
- Structural reorganization of sections

### When a Revision Plan is NOT Required
- Fixing a typo or single word
- Adding a [TODO] or [VERIFY] marker
- Adjusting paragraph wording without changing meaning
- Correcting a term per the glossary

### Revision Plan Format

```
REVISION PLAN
=============

Trigger: [What the user requested]

Changes:
  1. [Section X.Y] — [What will change and why]
  2. [Section X.Z] — [What will change and why]
  ...

Preserved (unchanged):
  - [List sections/content that will NOT be modified]

Impact on CN-EN alignment:
  - [Describe how both versions will be updated in sync]

Risks:
  - [Any potential issues: numbering shifts, broken cross-references, etc.]

Proceed? [Wait for user confirmation]
```

---

## MethodSpec Template

```
METHODSPEC v2.0
===============

1. PAPER METADATA
   - Title (working): ...
   - Target journal/conference: ...
   - Model name / abbreviation: ...
   - Paper type: [surrogate model / spatiotemporal prediction / LLM-enhanced / risk assessment / other]

   DoD:
   [ ] Model name is specified (or marked [TBD])
   [ ] Paper type is identified (determines section hierarchy per methodology_outline.md)

2. PROBLEM DEFINITION
   - Physical problem: ...
   - Engineering context: [excavation / tunnelling / foundation / slope / other]
   - Input variables: [list with symbols and units from notation.md]
   - Output variables: [list with symbols and units]
   - Key assumptions: ...
   - Physical constraints: [if any — boundary conditions, conservation laws, etc.]

   DoD:
   [ ] Physical problem stated in 1-2 sentences
   [ ] All input variables listed with symbols AND units
   [ ] All output variables listed with symbols AND units
   [ ] Every symbol matches notation.md conventions (or new symbol is defined)
   [ ] Units match hard_memory.json standard_units

3. FRAMEWORK OVERVIEW
   - Number of stages/modules: ...
   - Stage names (in order): ...
   - Data flow summary: [input] -> [stage 1] -> [stage 2] -> ... -> [output]
   - Figure reference: Figure [N]
   - Overview paragraph draft: [1 paragraph, ~100-150 words, with numbered steps]

   DoD:
   [ ] Number of stages matches the user's description
   [ ] Stage names are consistent (will be used as subsection titles)
   [ ] Data flow is a clear pipeline with no ambiguous connections
   [ ] Framework figure is referenced
   [ ] Overview paragraph follows user_style_profile.md Section 1.1 pattern

4. PHYSICAL / MECHANICAL MODEL (if applicable)
   - Model type: [elastic foundation beam / FEM / analytical / empirical / none]
   - Governing equations: [list equation IDs]
   - Boundary conditions: ...
   - Simplifying assumptions: ...
   - Parameters: [list with symbols, descriptions, and units]

   DoD:
   [ ] Governing equations are sourced from user's notes/code (not fabricated)
   [ ] Every parameter has symbol + unit + description
   [ ] Assumptions are explicitly stated (not implicit)
   [ ] If no physics model: this section is marked "N/A — pure data-driven approach"

5. DATA
   - Source: [simulation / field monitoring / hybrid / public dataset]
   - Generation method: [FEM parametric / real-world monitoring / synthetic / ...]
   - Total samples: ...
   - Input features (with dimensions): ...
   - Output targets (with dimensions): ...
   - Split ratio: train/val/test = .../.../ ...
   - Preprocessing: [normalization method, missing data handling, augmentation]
   - Data quality notes: [noise level, class balance, temporal resolution]

   DoD:
   [ ] Data source is from user input (not assumed)
   [ ] Total sample count is from user input or marked [TBD]
   [ ] Split ratio is from user input or marked [TBD]
   [ ] Input/output dimensions are from code or marked [TBD]
   [ ] Preprocessing method is from code/notes or marked [TBD]

6. MODEL ARCHITECTURE
   - Architecture type: [GAN / GCN / Transformer / hybrid / ...]
   - Total components: ...
   - Component list:
     * Component A: [name, purpose, key layers, input/output dims, activation]
     * Component B: [name, purpose, key layers, input/output dims, activation]
     * Component C: [name, purpose, key layers, input/output dims, activation]

   DoD:
   [ ] Every component has a clear name that will become a sub-subsection title
   [ ] Input/output dimensions are from code or marked [TBD]
   [ ] Activation functions are from code or marked [TBD]
   [ ] Layer counts are from code or marked [TBD]
   [ ] Architecture type matches the user's description

7. LOSS FUNCTION
   - Total loss formulation: L = ...
   - Components:
     * L_1: [name, formulation, purpose]
     * L_2: [name, formulation, purpose]
   - Weighting coefficients: [symbols and values]
   - Gradient penalty / regularization terms: ...

   DoD:
   [ ] Loss formulation is from code (not assumed)
   [ ] Each loss component has a clear name and purpose
   [ ] Weighting coefficients are from code or marked [TBD]
   [ ] All symbols in the loss are defined

8. TRAINING CONFIGURATION
   - Optimizer: ...
   - Learning rate: ... [scheduler: ...]
   - Batch size: ...
   - Epochs: ...
   - Early stopping: [yes/no, patience: ...]
   - Weight decay: ...
   - Hardware: [GPU type, count]
   - Framework: [PyTorch / TensorFlow / ...]
   - Random seed: ...

   DoD:
   [ ] Every value is from code/config or marked [TBD]
   [ ] If both notes and code provide a value, code value is used + conflict logged
   [ ] Optimizer type matches code exactly (Adam vs AdamW vs SGD)

9. EVALUATION METRICS
   - Metric list with formulas: [RMSE = ..., MAE = ..., ...]
   - Baseline models: [list with full names and abbreviations]
   - Comparison setup: [same dataset split, same preprocessing, same hardware?]

   DoD:
   [ ] Metric names match term_glossary.yml
   [ ] Baseline model names are from user input (not suggested by AI)
   [ ] Metric formulas are standard (from notation.md or textbook)

10. CONFLICTS & GAPS
    - Conflicts: [List every conflict between notes and code, with resolution]
    - Gaps: [List every missing value with [TBD] marker]
    - Assumptions: [List any standard assumptions the AI made, for user verification]
    - Citation gaps: [List every reference that needs full citation info]

    DoD:
    [ ] Every [TBD] has a specific description of what the user needs to provide
    [ ] Every conflict shows both values and which was used (code wins)
    [ ] No silent assumptions — every inference is logged here
```

---

## MethodSpec Review Gate

After generating the MethodSpec, present it to the user with this prompt:

"MethodSpec is ready for review. Please check:
1. Are all values correct? (Especially Section 8: Training Configuration)
2. Are there any missing components not captured above?
3. Should I proceed to generate the Chinese and English methodology sections?"

DO NOT proceed to DRAFT until the user confirms. If the user provides corrections,
update the MethodSpec and re-present. Log any corrections in error_log.md.
