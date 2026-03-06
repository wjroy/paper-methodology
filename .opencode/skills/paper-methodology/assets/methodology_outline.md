# Methodology Outline (Base Skeleton + Pattern Overlays)

Purpose: provide a reusable section-planning scaffold without forcing a single
invariant order for all papers.

Scope boundary: this file defines only structure skeleton + pattern overlay
hooks. It does not own terminology mapping, style tuning, or memory rules.

## A. Base Skeleton

Use this as the default scaffold in PLAN, then apply one selected overlay from
`methodology_patterns.yml`.

1) Problem definition and objective
- Engineering target, prediction/assessment output, scope.

2) Framework overview
- One paragraph with method name and figure anchor.
- Brief module map in execution order.

3) Data and representation pipeline
- Data sources, preprocessing/transformation, graph/text/feature construction.

4) Core modeling modules
- Architecture and module interactions in pipeline order.

5) Objective/constraints and optimization
- Loss terms, physical constraints, quantile/scoring objectives.

6) Evaluation anchors
- Metrics/baselines and (optional) deployment notes.

## B. Pattern Overlays

Apply exactly one primary overlay (allow 1-2 fallback overlays when hybrid).

- `framework-first`
  - Keep Base order; emphasize concise overview and module-by-module unfolding.

- `physics-mechanism-first`
  - Move mechanical formulation before general architecture details.
  - Keep architecture section focused on how mechanics is injected.

- `data-transformation-first`
  - Expand Section 3 (data/representation) and place it before architecture.
  - Keep architecture section concise and downstream-oriented.

- `fusion-pattern`
  - Split Section 4 into modality-specific encoders + fusion block.
  - Make cross-modal interaction logic explicit.

- `weighting-scoring-decision`
  - Expand Sections 1 and 5 around risk-level scoring/decision rules.
  - Architecture details are optional if not central.

- `constraint-loss-first`
  - Surface key constraint/loss rationale early (end of Section 2 or start of 4).
  - Tie metrics directly to objective behavior.

## C. Hard Guards

- Do not claim a universal invariant section order across all own papers.
- Do not force a physics module when method has no explicit physical prior.
- Do not force deep-learning architecture detail for decision-centric methods.
- If required hard facts are missing, keep placeholders and register TODO/VERIFY.

## D. Section-Level Refinement Overlay

Use this overlay when user locks scope to a target section/subsection.

1) Keep global chapter structure unchanged by default.
2) Update only target-linked MethodSpec entries.
3) Allow only minimal linked edits outside target scope:
- terminology normalization,
- symbol/equation numbering repair,
- one-hop context bridge for continuity.
4) Preserve CN/EN alignment and traceability for updated scope.
