# paper-methodology Skill

OpenCode skill for generating bilingual (Chinese + English) Methodology/Methods
sections for SCI papers in geotechnical AI.

## What This Skill Does

Given user notes plus real code/config, the skill runs a lightweight,
gate-controlled workflow and outputs:

1. MethodSpec (single source of truth)
2. Chinese Methodology (plain text)
3. English Methodology (plain text)
4. TODO/VERIFY + audit summary

## Core Guarantees

- MethodSpec-first (no prose before MethodSpec)
- code/config > notes on conflicts
- no fabrication of parameters, results, baselines, or citations
- strict CN-EN structural/value alignment
- compact runtime context (targeted asset loading only)

## Workflow (v3.3)

The main workflow is fixed as three phases:

GATHER -> PLAN -> WRITE_AUDIT

- GATHER: extract hard facts, detect conflicts/gaps
- PLAN: choose methodology pattern, build section plan, generate MethodSpec
- WRITE_AUDIT: draft CN+EN and run compact 6-pass audit

Confirmation gate:
- By default, Phase C runs only after user confirms MethodSpec.
- Skip is allowed only with explicit instructions (e.g., "skip confirmation").

## Pattern Library and Outline

Pattern library is used in PLAN to avoid a one-size-fits-all template:

- `assets/methodology_patterns.yml`
  - framework-first
  - physics-mechanism-first
  - data-transformation-first
  - fusion-pattern
  - weighting-scoring-decision
  - constraint-loss-first

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
- `assets/reference_papers/*.txt` (top relevant subset only)

Note:

- `assets/upstream_prompt_pack.md` is no longer used at runtime.
- Required minimum rendering/humanizer/redline rules are inlined in
  `SKILL.md` and `methods-bilingual.md`.

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

Current suite size: 13 tests, covering:

- core workflow behavior
- style/error-log consistency
- MethodSpec Source/Confidence traceability
- PLAN confirmation gate and skip-gate behavior
- pattern library selection
- inlined humanizer/polish/redline behavior (without prompt-pack dependency)

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
