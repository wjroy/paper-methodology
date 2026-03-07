# Heading Style Profile

Purpose: define heading naming conventions for methodology section/subsection
titles. This file is the heading-specific counterpart to `style_profile.md`
(which covers prose style).

Scope: methodology section headings only (not abstract, introduction, or
discussion headings).

## 0. Calibration Status

Rule-refinement evidence scope:
- Calibrated from all own papers (01-05) for stylistic boundary.
- Calibrated from all other reference papers (06-18) for field-wide heading
  diversity and mature naming patterns.
- Runtime generation uses only 2-3 own + 2-3 other papers most relevant to
  the current task's methodology pattern and technical domain.

## 1. Heading Tone

- Academic-technical: formal but not verbose.
- Headings should be informative (reader can infer section content from heading
  alone) but not sentence-length.
- Avoid promotional or evaluative language in headings ("Novel X", "Advanced Y",
  "Superior Z").
- Avoid generic placeholder headings ("Details", "Other", "Additional").

## 2. Phrase Type

Primary convention (own papers 01-05): **noun phrases exclusively**.
- All five own papers use noun-phrase headings without exception.
- Verb-phrase headings are allowed only when the selected methodology pattern
  explicitly uses step-style markers (e.g., weighting-scoring-decision pattern
  with "Step X:" labels, following 05-own-TSFRA convention).

Acceptable noun-phrase structures:
- "X of Y" (e.g., "Framework of PitGAN", "Architecture of generator")
- "X-based Y" (e.g., "Attention-based fusion")
- "X for Y" purpose clause (e.g., "EGCN module for spatial dependency modeling")
- Direct component naming (e.g., "Graph WaveNet", "Text Transformer")
- Compound descriptors (e.g., "Adaptive physics-informed edge-feature generation")

## 3. Preferred Length

Own-paper range (calibrated from 01-05):
- Short (2-4 words): component-specific headings, evaluation headings.
  Examples: "Architecture of generator", "Model evaluation", "Quantile prediction"
- Medium (5-8 words): standard subsection headings.
  Examples: "Overall framework of PI-ETGCN", "Multi-source data collection and
  node-feature integration"
- Long (9+ words): complex pipeline step headings. Use sparingly.
  Examples: "Generation of PitGAN data for modeling foundation pit excavation"

Default preference: medium (5-8 words). Use short for terse component labels
when the architecture is modular; use long only when the pipeline step requires
disambiguation.

## 4. Method/Model Name in Headings

Own-paper convention: the method/model name appears in at least one heading
(typically the framework overview heading) and optionally in one or two core
architecture headings.

Rules:
- Framework overview heading: SHOULD include method name.
  Pattern: "Overall framework of [Method]" or "Framework of [Method]" or
  "[Method] implementation for [purpose]"
- Core architecture heading: MAY include method name if it disambiguates.
- Do not force method name into every heading — this becomes repetitive.
- Abbreviation with parenthetical definition is acceptable in one heading
  (e.g., "Graph WaveNet-Transformer-Attention fusion (GTAF) model").

## 5. Sibling-Heading Symmetry

Sibling subsections at the same hierarchical level should use a consistent
phrase structure. Do not randomly mix structural patterns within the same level.

Acceptable symmetry patterns:
- All "X of Y": "Architecture of generator" / "Architecture of discriminator"
- All "X module for Y": "EGCN module for spatial modeling" / "GRU module for
  temporal modeling"
- All direct naming: "Graph WaveNet" / "Text Transformer" / "Attention-based fusion"
- All "Construction of X": "Construction of heterogeneous graph" / "Construction
  of adjacency matrices"

Violations to avoid:
- "Architecture of generator" alongside "The discriminator design process"
- "EGCN spatial module" alongside "Temporal dependency modeling with GRU"

Exception: when sibling sections genuinely differ in nature (e.g., a data
section and an architecture section under the same parent), the phrase structure
may differ.

## 6. Preferred Keywords in Headings

From own papers (01-05), frequently used heading keywords:
- Framework / overall framework
- Architecture
- Module
- Generation / construction
- Modeling / model
- Feature / representation
- Loss function / objective
- Evaluation / metrics

From other papers (06-18), additional mature heading keywords:
- Encoder / decoder
- Fusion / interaction
- Prediction / estimation
- Fine-tuning / adaptation
- Preprocessing / data preparation
- Sensitivity analysis

## 7. Headings to Avoid

- "Methodology" or "Method" as a subsection heading (reserved for the main section).
- "Background" or "Preliminaries" inside the methodology (these belong in a
  separate section or introduction).
- "Implementation details" as a heading for training config (prefer moving
  training details to Case Study unless user explicitly requests otherwise).
- Headings that are too generic to be informative: "Model", "Data", "Results"
  (add a qualifier: "Prediction model architecture", "Monitoring data
  representation").
- Headings that duplicate the parent heading in different words.
- Headings borrowed verbatim from reference papers.

## 8. Sub-Subsection Heading Conventions

Own papers use three different sub-subsection styles:
- Decimal numbering (2.x.x): used in 01-PitGAN, 03-THGAN.
- Parenthesized numbering (1), (2), (3): used in 02-PI-ETGCN, 04-LLM-GNN.
- Lettered labels (a), (b), (c): used in 03-THGAN for fine-grained components.
- "Step X:" markers: used in 05-TSFRA for sequential decision processes.

Rule: choose one sub-subsection style per paper and apply it consistently.
Do not mix decimal sub-subsections with parenthesized numbering in the same
chapter.

## 9. CN-EN Heading Alignment

- CN and EN headings must be structurally aligned (same numbering, same level).
- CN headings should be the semantic equivalent, not word-by-word translation.
- Technical terms may stay in English within CN headings where natural
  (e.g., "PI-ETGCN 整体框架" is acceptable).
- Abbreviations should appear in both versions identically.

## 10. Runtime Use Checklist

Before heading generation:
1) Load this profile
2) Load heading_patterns.yml for pattern-specific templates
3) Identify the selected methodology pattern
4) Retrieve 2-3 own + 2-3 other papers relevant to the pattern

During heading generation:
1) Apply phrase-type and symmetry rules
2) Check method name placement
3) Verify heading length is within preferred range
4) Provide alternatives for ambiguous sections

After heading generation:
1) Verify CN-EN heading alignment
2) Verify no verbatim copying from reference papers
3) Present Heading Plan for user confirmation
