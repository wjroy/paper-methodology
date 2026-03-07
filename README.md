# paper-methodology Skill

OpenCode skill for generating bilingual (Chinese + English) Methodology/Methods
sections for SCI papers in geotechnical AI.

## What This Skill Does

Given user notes plus real code/config, the skill runs a lightweight,
gate-controlled workflow and outputs:

1. MethodSpec (single source of truth)
2. Heading Plan (confirmed before drafting)
3. Chinese Methodology (plain text)
4. English Methodology (plain text)
5. TODO/VERIFY + audit summary

## Core Guarantees

- MethodSpec-first (no prose before MethodSpec)
- Heading Plan confirmed before body drafting
- code/config > notes on conflicts
- no fabrication of parameters, results, baselines, or citations
- strict CN-EN structural/value alignment
- compact runtime context (targeted asset loading only)

## Workflow (v3.7)

The main workflow is fixed as three phases:

GATHER -> PLAN -> WRITE_AUDIT

- GATHER: extract hard facts, detect conflicts/gaps
- PLAN: choose methodology pattern, build section plan, generate MethodSpec,
  then generate Heading Plan (both require user confirmation before drafting)
- WRITE_AUDIT: draft CN+EN under confirmed headings and run compact 7-pass audit

Confirmation gates:
- By default, Phase C runs only after user confirms both MethodSpec and
  Heading Plan.
- Skip is allowed only with explicit instructions (e.g., "skip confirmation",
  "skip heading confirmation").

## Execution Modes

- **Mode A**: Full-chapter generation (MethodSpec + Heading Plan + CN/EN + audit)
- **Mode B**: Section-level refinement (local scope lock, MethodSpec delta)
- **Mode C**: Heading-plan only (MethodSpec + Heading Plan, no body text)
- **Mode D**: Heading-refinement (update existing headings with annotations)
- **Mode E**: Lock-headings-and-draft (body text under pre-approved headings)

## Pattern Library and Outline

Pattern library is used in PLAN to avoid a one-size-fits-all template:

- `assets/methodology_patterns.yml`
  - framework-first
  - physics-mechanism-first
  - data-transformation-first
  - fusion-pattern
  - weighting-scoring-decision
  - constraint-loss-first

Heading naming patterns (pattern-specific heading templates):

- `assets/heading_patterns.yml`

Heading style conventions (naming tone, phrase type, length, symmetry):

- `assets/heading_style_profile.md`

Outline file provides only base skeleton + overlay linkage:

- `assets/methodology_outline.md`

## MethodSpec Traceability

MethodSpec traceability is mandatory:

- Every hard-fact field (Sections 2-9) must include:
  - `Source`
  - `Confidence` (OK / NEEDS_VERIFY)
- Blank source is an audit FAIL.
- `[TBD]` must be mirrored in Conflicts/Gaps and TODO/VERIFY.

Template:

- `assets/methodspec_template.md`

## Runtime Assets (Current)

Always read:

- `assets/style_profile.md`
- `assets/error_log.md`
- `assets/memory/hard_memory.json`
- `assets/memory/soft_memory.json`

Read on-demand:

- `assets/methodspec_template.md`
- `assets/term_glossary.yml`
- `assets/notation.md`
- `assets/methodology_patterns.yml`
- `assets/methodology_outline.md`
- `assets/heading_style_profile.md`
- `assets/heading_patterns.yml`
- `assets/reference_papers/*.txt` (top relevant subset only)

## Repository Structure (Current)

```
.opencode/
├── skills/paper-methodology/
│   ├── SKILL.md
│   └── assets/
│       ├── memory/
│       │   ├── hard_memory.json
│       │   └── soft_memory.json
│       ├── reference_papers/
│       ├── methodology_patterns.yml
│       ├── methodology_outline.md
│       ├── methodspec_template.md
│       ├── heading_style_profile.md
│       ├── heading_patterns.yml
│       ├── style_profile.md
│       ├── term_glossary.yml
│       ├── notation.md
│       └── error_log.md
├── commands/
│   └── methods-bilingual.md
└── regression/
    └── paper-methodology-tests.md
```

## Testing

Regression tests are maintained in:

- `.opencode/regression/paper-methodology-tests.md`

Current suite size: 23 tests, covering:

- core workflow behavior (Tests 1-5)
- style/error-log consistency (Tests 6-8)
- MethodSpec Source/Confidence traceability and PLAN gate behavior (Tests 9-11)
- pattern library selection and inlined humanizer/polish/redline (Tests 12-13)
- section-level refinement scope-lock and MethodSpec sync (Tests 14-15)
- logic-enrichment continuity and anti-hallucination guard (Tests 16-17)
- calibration-scope split (Test 18)
- heading plan gate, multiple candidates, refinement isolation,
  pattern-awareness, and skip-heading behavior (Tests 19-23)

## Usage

Use command:

```
/methods-bilingual
```

Then provide:

- notes (plain-language method details)
- code/config paths (if available)
- optional target journal

## Scope and Limits

- Domain: geotechnical AI only
- Section scope: Methodology/Methods only
- Output: plain text (Word-ready)
- Citations: unverifiable references remain `[CITATION NEEDED]`
