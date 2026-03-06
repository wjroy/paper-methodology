---
description: >
  Generate bilingual (CN + EN) Methodology section for a geotechnical AI paper.
  Uses the 3-phase workflow: GATHER → PLAN → WRITE_AUDIT.
  Produces: MethodSpec → Chinese Methods → English Methods → TODO/VERIFY list.
---

# Bilingual Methods Section Generator (v3.3)

You are about to generate a complete Methodology/Methods section for a geotechnical
AI paper. Follow the `paper-methodology` skill's 3-phase mandatory workflow strictly.

## Your Input

Please provide the following (paste below or reference file paths):

**1. Research notes or outline** (required):
$ARGUMENTS

**2. Code/config files** (if available):
- Model definition script path: [paste or describe]
- Training script path: [paste or describe]
- Config file path: [paste or describe]

**3. Target journal/conference** (optional):
[e.g., Tunnelling and Underground Space Technology, Computers and Geotechnics]

## Workflow

Execute the paper-methodology skill's 3-phase mandatory workflow:

### Phase A: GATHER

Goal: collect facts and constraints before writing.

A1. Read runtime assets:
- Always read: `assets/style_profile.md`, `assets/error_log.md`,
  `assets/memory/hard_memory.json`, `assets/memory/soft_memory.json`
- On-demand: `assets/term_glossary.yml`, `assets/notation.md`,
  `assets/methodology_patterns.yml`, `assets/methodology_outline.md`,
  `assets/reference_papers/*.txt` (top 3-5 relevant only),
  `assets/methodspec_template.md`

A2. Parse all provided materials — notes, code, config, figures. Extract:
- Problem + engineering context
- Inputs/outputs
- Model components
- Loss definitions
- Training setup (if provided)
- Metrics + baselines
- Figure/table anchors (if provided)

A3. Detect conflicts (notes vs code/config) and gaps (missing hard facts).
Code/config always wins over notes. Log conflicts explicitly.

A4. Build lightweight Methodology Map:
- Extract keywords from user content (open extraction)
- Retrieve only top 3-5 relevant reference papers
- Learn structure logic only (never copy values/content)

A5. If required hard facts are missing and cannot be inferred safely,
ask one compact Clarification Block before proceeding to Phase B.

### Phase B: PLAN (MethodSpec gate)

Goal: create a single source of truth for CN and EN drafting.

B1. Select one primary methodology pattern from `assets/methodology_patterns.yml`
with brief rationale; include 1-2 fallback patterns.

B2. Build section plan from base skeleton + selected overlay in
`assets/methodology_outline.md`.

B3. Generate the structured MethodSpec using `assets/methodspec_template.md`.
For each hard-fact field in Sections 2-9, include Source and Confidence.
Blank Source on any hard-fact field = Audit Pass 6 FAIL.

B4. Present MethodSpec and enforce confirmation gate.

**MANDATORY GATE**: Do NOT proceed to Phase C until the user explicitly confirms
with "CONFIRM", "OK", "proceed", or equivalent.

Skip-gate exception only when user explicitly says:
- "skip confirmation" / "跳过确认"
- "generate directly" / "直接生成"
- "no review needed" / "无需审核"

### Phase C: WRITE_AUDIT

Goal: draft CN and EN from MethodSpec, then run compact audit.

C1. Draft Chinese Methodology (plain text, full-width punctuation, no Markdown).

C2. Draft English Methodology (present tense, mirrors CN structure exactly).

C3. Ask humanizer question: "English version is ready. Apply de-AI humanizer pass?"
Do not auto-apply. If user agrees, apply minimal de-AI constraints:
- Keep all technical content unchanged (numbers/symbols/equations/references)
- Remove filler/promotional wording and mechanical connector stacking
- Keep original if already natural

C3.1 Optional ask-first refinements:
- Expand: +5 to +15 words without adding unsourced facts
- Compress: -5 to -15 words while preserving all technical content
- Polish: improve clarity and grammar without changing technical meaning

C3.2 Run minimal logic-redline check:
- Check only contradictions, core-term inconsistency, and severe grammar
- Do not report style-only issues in this pass

C4. Run compact 6-pass audit:
1. Terminology consistency (glossary + hard_memory)
2. Numerical consistency (MethodSpec vs CN vs EN)
3. Equation/symbol consistency (notation + where blocks)
4. Structural alignment (CN vs EN)
5. Error-log compliance (no repeated mistakes)
6. Traceability — every hard-fact field in MethodSpec Sections 2-9 must have
   populated Source and Confidence. Blank Source = FAIL. Every [TBD] Source
   must have a matching entry in Section 10 and TODO/VERIFY.

Fix FAIL items before delivery. Put unresolved items in TODO/VERIFY.

C5. Pre-delivery gate checklist:
- G1: Phase A completed
- G2: MethodSpec produced
- G3: Confirmation satisfied OR explicit skip-gate instruction found
- G4: CN and EN drafted from the same MethodSpec
- G5: 6-pass audit executed

If any gate is false, stop and repair before final output.

## Revision Policy

- Small revision (<3 paragraphs, no structure change): revise directly.
- Large revision (>=3 paragraphs or structural): present Revision Plan first,
  then wait for user approval.

## Output Format

Produce all 4 outputs in sequence:
1. MethodSpec (structured, with Source and Confidence fields)
2. Chinese Methodology (plain text)
3. English Methodology (plain text)
4. TODO/VERIFY List + Audit Summary
