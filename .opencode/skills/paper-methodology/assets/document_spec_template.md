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
     Source: [user notes / code comments / config file]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Engineering context: [excavation / tunnelling / foundation / slope / other]
     Source: [user notes / domain inference from problem description]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Input variables: [list with symbols and units from notation.md]
     Source: [code: model input definition @file.py#L10-15 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Output variables: [list with symbols and units]
     Source: [code: model output definition @file.py#L20-25 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Key assumptions: ...
     Source: [user notes / inferred from physics model]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Physical constraints: [if any — boundary conditions, conservation laws, etc.]
     Source: [user notes / physics model documentation]
     Confidence: [OK / NEEDS_VERIFY]

   DoD:
   [ ] Physical problem stated in 1-2 sentences WITH Source
   [ ] All input variables listed with symbols AND units WITH Source
   [ ] All output variables listed with symbols AND units WITH Source
   [ ] Every symbol matches notation.md conventions (or new symbol is defined)
   [ ] Units match hard_memory.json standard_units
   [ ] Every hard fact has Source field populated (not empty)
   [ ] Confidence is OK for all items OR flagged NEEDS_VERIFY with explanation

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
     Source: [user notes / code comments]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Generation method: [FEM parametric / real-world monitoring / synthetic / ...]
     Source: [user notes / inferred from data source]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Total samples: ...
     Source: [code: dataset.__len__() @data.py#L50 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Input features (with dimensions): ...
     Source: [code: input shape @model.py#L10 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Output targets (with dimensions): ...
     Source: [code: output shape @model.py#L20 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Split ratio: train/val/test = .../.../ ...
     Source: [code: train_test_split @train.py#L30 / config.yaml#L15]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Preprocessing: [normalization method, missing data handling, augmentation]
     Source: [code: preprocessing pipeline @data.py#L100 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Data quality notes: [noise level, class balance, temporal resolution]
     Source: [user notes / inferred from data inspection]
     Confidence: [OK / NEEDS_VERIFY]

   DoD:
   [ ] Data source is from user input (not assumed) WITH Source
   [ ] Total sample count is from user input or marked [TBD] WITH Source
   [ ] Split ratio is from user input or marked [TBD] WITH Source
   [ ] Input/output dimensions are from code or marked [TBD] WITH Source
   [ ] Preprocessing method is from code/notes or marked [TBD] WITH Source
   [ ] Every numerical value has Source field populated

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
     Source: [@train.py#L45 / @config.yaml#L10]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Learning rate: ... [scheduler: ...]
     Source: [@config.yaml#L12]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Batch size: ...
     Source: [@config.yaml#L8]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Epochs: ...
     Source: [@config.yaml#L15 / @train.py#L50]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Early stopping: [yes/no, patience: ...]
     Source: [@train.py#L60 / user notes]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Weight decay: ...
     Source: [@config.yaml#L18]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Hardware: [GPU type, count]
     Source: [user notes / inferred from training logs]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Framework: [PyTorch / TensorFlow / ...]
     Source: [code: import statements @train.py#L1-5]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Random seed: ...
     Source: [@train.py#L10 / @config.yaml#L5]
     Confidence: [OK / NEEDS_VERIFY]

   DoD:
   [ ] Every value is from code/config or marked [TBD] WITH Source
   [ ] If both notes and code provide a value, code value is used + conflict logged WITH both Sources
   [ ] Optimizer type matches code exactly (Adam vs AdamW vs SGD) WITH Source
   [ ] All Source fields are specific (e.g., @config.yaml#L10 not just "config file")

9. EVALUATION METRICS
   - Metric list with formulas: [RMSE = ..., MAE = ..., ...]
     Source: [user notes / code: evaluation.py#L20-30]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Baseline models: [list with full names and abbreviations]
     Source: [user notes / code: baselines.py]
     Confidence: [OK / NEEDS_VERIFY]
   
   - Comparison setup: [same dataset split, same preprocessing, same hardware?]
     Source: [user notes / inferred from experimental setup]
     Confidence: [OK / NEEDS_VERIFY]

   DoD:
   [ ] Metric names match term_glossary.yml
   [ ] Baseline model names are from user input (not suggested by AI) WITH Source
   [ ] Metric formulas are standard (from notation.md or textbook)
   [ ] All Source fields populated for metrics and baselines

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
2. Are all Source fields populated for hard facts?
3. Are there any missing components not captured above?
4. Reply CONFIRM or OK to proceed to DRAFT, or provide corrections."

DO NOT proceed to DRAFT until the user confirms. If the user provides corrections,
update the MethodSpec and re-present. Log any corrections in error_log.md.
