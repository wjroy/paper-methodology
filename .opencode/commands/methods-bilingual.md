---
description: >
  Generate or refine bilingual (CN + EN) Methodology for a geotechnical AI paper.
  Uses the 3-phase workflow: GATHER → PLAN (MethodSpec + Heading Plan) → WRITE_AUDIT.
  Supports full-chapter generation, section-level refinement, and heading-only modes.
  Produces: MethodSpec → Heading Plan → Chinese Methods → English Methods → TODO/VERIFY list.
---

# Bilingual Methods Section Generator (v3.7)

You are about to run the `paper-methodology` workflow for a geotechnical AI paper.
Follow the skill's 3-phase mandatory workflow strictly, and first determine mode.

Calibration scope note (must follow):
- Rule refinement / skill updates are calibrated on all own papers 01-05.
- Runtime generation stays lightweight and uses only the most relevant own papers
  (default top 2-3, expand only when needed).

## Your Input

Choose one mode and provide matching inputs.

### Mode A: Full-chapter generation (existing behavior)

Provide the following (paste below or reference file paths):

**1. Research notes or outline** (required):
$ARGUMENTS

**2. Code/config files** (if available):
- Model definition script path: [paste or describe]
- Training script path: [paste or describe]
- Config file path: [paste or describe]

**3. Target journal/conference** (optional):
[e.g., Tunnelling and Underground Space Technology, Computers and Geotechnics]

### Mode B: Section-level refinement (existing behavior)

Use this template:

- target_section_or_subsection: [e.g., 3.2 / 3.2.1 / "Loss Function"]
- operation_type: [expand | rewrite | correct | bilingual-sync]
- existing_section_text_cn: [paste existing CN subsection text or N/A]
- existing_section_text_en: [paste existing EN subsection text or N/A]
- added_notes: [new plain-language details]
- added_code_or_config_paths: [list paths; optional but preferred]
- optional_context: [adjacent paragraph or cross-reference anchors]

Local-mode directive:
- This is a local refinement request, not a full-chapter rewrite.
- Update only target-related MethodSpec fields and target subsection prose.
- Keep other sections unchanged unless minimal linked edits are required for
  term/symbol/numbering/cross-reference consistency.

### Mode C: Heading-plan (generate headings without body text)

Use this template:

- operation_type: heading-plan
- research_notes: [paste notes or reference file paths]
- code_or_config_paths: [list paths; optional but preferred]
- style_preference: [optional — concise / framework-oriented / mechanism-oriented
  / engineering-style / decision-step / more academic / etc.]
- target_journal: [optional]

This mode runs Phase A (GATHER) and Phase B through Heading Plan, then stops.
Output: MethodSpec + Heading Plan. No body text is drafted.

### Mode D: Heading-refinement (refine existing headings without body rewrite)

Use this template:

- operation_type: heading-refinement
- existing_headings: [paste current heading list]
- target_section_or_subsection: [optional — for partial heading refinement]
- requested_changes: [describe desired changes, e.g., "make Section 3.3 more
  mechanism-oriented", "shorten all subsection headings", "add fusion semantics"]
- style_preference: [optional — concise / framework-oriented / mechanism-oriented
  / engineering-style / decision-step / more academic / etc.]

This mode re-evaluates headings against MethodSpec, selected pattern, and heading
naming rules. Output: updated Heading Plan with change annotations. No body text
is rewritten.

### Mode E: Lock-headings-and-draft (draft body under approved headings)

Use this template:

- operation_type: lock-headings-and-draft
- approved_headings: [paste confirmed heading list]
- research_notes: [paste notes or reference file paths]
- code_or_config_paths: [list paths; optional but preferred]
- existing_methodspec: [optional — paste if already generated]

This mode uses the locked heading structure as skeleton for Phase C drafting.
Headings are not renamed or reordered during drafting.

## Workflow

Execute the paper-methodology skill's 3-phase mandatory workflow.

Mode routing:
- If user provides full notes without target subsection lock, run Mode A.
- If user provides `target_section_or_subsection` with operation_type expand/rewrite/correct/bilingual-sync, run Mode B (local scope lock).
- If user provides `operation_type: heading-plan`, run Mode C (heading-only).
- If user provides `operation_type: heading-refinement`, run Mode D (heading refinement).
- If user provides `operation_type: lock-headings-and-draft`, run Mode E (locked drafting).

### Phase A: GATHER

Goal: collect facts and constraints before writing.

A1. Read runtime assets:
- Always read: `assets/style_profile.md`, `assets/error_log.md`,
  `assets/memory/hard_memory.json`, `assets/memory/soft_memory.json`
- On-demand: `assets/term_glossary.yml`, `assets/notation.md`,
  `assets/methodology_patterns.yml`, `assets/methodology_outline.md`,
  `assets/reference_papers/*.txt` (top 2-3 relevant by default; expand only when needed),
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

If Mode B:
- Extract and validate target-related facts only.
- Keep non-target facts unchanged unless dependency repair is required.

A4. Build lightweight Methodology Map:
- Extract keywords from user content (open extraction)
- Retrieve only top 2-3 relevant own papers by default (expand to top 5 only
  for hybrid/ambiguous architecture)
- Learn structure logic only (never copy values/content)

A5. If required hard facts are missing and cannot be inferred safely,
ask one compact Clarification Block before proceeding to Phase B.

### Phase B: PLAN (MethodSpec gate + Heading Plan gate)

Goal: create a single source of truth for CN and EN drafting, then plan headings.

B1. Select one primary methodology pattern from `assets/methodology_patterns.yml`
with brief rationale; include 1-2 fallback patterns.

B2. Build section plan from base skeleton + selected overlay in
`assets/methodology_outline.md`.

B3. Generate the structured MethodSpec using `assets/methodspec_template.md`.
For each hard-fact field in Sections 2-9, include Source and Confidence.
Blank Source on any hard-fact field = Audit Pass 6 FAIL.

If Mode B:
- Update only MethodSpec entries linked to target section/subsection.
- Do not regenerate unrelated MethodSpec content.
- Keep Source/Confidence traceability for every updated field.
- Return a compact MethodSpec delta block with `UNCHANGED` vs `UPDATED` tags.

B4. Present MethodSpec and enforce MethodSpec confirmation gate.

**MANDATORY GATE**: Do NOT proceed to Heading Plan or Phase C until the user
explicitly confirms with "CONFIRM", "OK", "proceed", or equivalent.

Skip-gate exception only when user explicitly says:
- "skip confirmation" / "跳过确认"
- "generate directly" / "直接生成"
- "no review needed" / "无需审核"

#### Phase B2: Heading Plan (after MethodSpec confirmation)

B5. Load heading naming assets (on-demand):
- `assets/heading_style_profile.md` (naming conventions)
- `assets/heading_patterns.yml` (pattern-specific heading templates)
- Retrieve 2-3 own papers + 2-3 other papers most relevant to the current
  task's methodology pattern (lightweight runtime retrieval).

B6. Generate Heading Plan:
- Use MethodSpec + selected pattern + heading naming rules.
- Produce numbered list of proposed section/subsection titles.
- For key sections with high ambiguity, provide 2-3 alternative candidates.
- Note heading style tendency when useful (concise / framework-oriented /
  mechanism-oriented / engineering-style / decision-step).

If Mode C (heading-plan): deliver Heading Plan and stop. Do not enter Phase C.
If Mode D (heading-refinement): re-evaluate existing headings against rules,
produce updated Heading Plan with change annotations, and stop.

B7. Present Heading Plan and enforce heading confirmation gate.

**MANDATORY GATE**: Do NOT proceed to Phase C until the user explicitly confirms
headings with "CONFIRM", "OK", "proceed", or equivalent.

Skip-heading exception only when user explicitly says:
- "skip heading confirmation" / "跳过标题确认"
- "generate directly" / "直接生成"
- "use default headings" / "使用默认标题"
- "no heading review needed" / "标题无需审核"

If Mode E (lock-headings-and-draft): use user's approved_headings directly
as the heading skeleton. Skip B5-B7 and proceed to Phase C.

### Phase C: WRITE_AUDIT

Goal: draft CN and EN from MethodSpec under approved headings, then run compact audit.

C1. Draft Chinese Methodology (plain text, full-width punctuation, no Markdown).
Use the approved Heading Plan as the structural skeleton. Do not rename or
reorder headings unless flagged as HEADING MISMATCH in TODO/VERIFY.

C2. Draft English Methodology (present tense, mirrors CN structure exactly).

If Mode B:
- Rewrite/expand/correct only the target CN/EN subsection.
- Keep non-target sections unchanged by default.

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

C3.3 Run logic-enrichment pass (targeted, source-grounded):
- Add only supportable implicit logic: module purpose, input -> operation ->
  output chain, and next-step handoff.
- For equations/loss/fusion/constraint mentions, state functional role in the
  pipeline.
- Never add new facts/parameters/citations/modules/results.
- If support is missing, keep placeholders and add TODO/VERIFY.

C4. Run compact 6-pass audit:
1. Terminology consistency (glossary + hard_memory)
2. Numerical consistency (MethodSpec vs CN vs EN)
3. Equation/symbol consistency (notation + where blocks)
4. Structural alignment (CN vs EN)
5. Error-log compliance (no repeated mistakes)
6. Traceability — every hard-fact field in MethodSpec Sections 2-9 must have
   populated Source and Confidence. Blank Source = FAIL. Every [TBD] Source
   must have a matching entry in Section 10 and TODO/VERIFY.

If Mode B, add local checks:
- Scope integrity: no unintended edits outside target scope
- Terminology/symbol/numbering consistency after local edit
- CN/EN alignment for updated subsection
- No unsourced values introduced

Fix FAIL items before delivery. Put unresolved items in TODO/VERIFY.

C5. Pre-delivery gate checklist:
- G1: Phase A completed
- G2: MethodSpec produced
- G3: MethodSpec confirmation satisfied OR explicit skip-gate instruction found
- G3.1: Heading Plan produced and confirmed OR explicit skip-heading instruction found
- G4: CN and EN drafted from the same MethodSpec under approved headings
- G5: 6-pass audit executed

If any gate is false, stop and repair before final output.

## Revision Policy

- Small revision (<3 paragraphs, no structure change): revise directly.
- Section-level refinement defaults to local update (Mode B).
- If new details force chapter-level structure changes, escalate to large revision
  with a Revision Plan first.
- Large revision (>=3 paragraphs or structural): present Revision Plan first,
  then wait for user approval.

## Output Format

Produce outputs in sequence (scope depends on mode):

Mode A (full-chapter):
1. MethodSpec (structured, with Source and Confidence fields)
2. Heading Plan (with alternatives for ambiguous sections)
3. Chinese Methodology (plain text, under approved headings)
4. English Methodology (plain text, under approved headings)
5. TODO/VERIFY List + Audit Summary

Mode B (section-level refinement):
- Updated MethodSpec entries for the target scope + updated target CN/EN subsection.
- Do not rewrite untouched sections.
- If any linked edit outside target scope is required, list each edit and reason
  explicitly (term/symbol/numbering/cross-reference bridge only).

Mode C (heading-plan):
1. MethodSpec (structured)
2. Heading Plan
- No body text output.

Mode D (heading-refinement):
1. Updated Heading Plan with change annotations (KEPT / RENAMED / ADDED /
   REMOVED / REORDERED)
- No body text output.

Mode E (lock-headings-and-draft):
1. MethodSpec (if not already provided)
2. Chinese Methodology (plain text, under locked headings)
3. English Methodology (plain text, under locked headings)
4. TODO/VERIFY List + Audit Summary
