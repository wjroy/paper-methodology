---
description: >
  Generate bilingual (CN + EN) Methodology section for a geotechnical AI paper.
  Uses the 6-step workflow: Analyze → Recall → Plan → Draft → Audit → Iterate.
  Produces: MethodSpec -> Chinese Methods -> English Methods -> TODO/VERIFY list.
---

# Bilingual Methods Section Generator (v2.0)

You are about to generate a complete Methodology/Methods section for a geotechnical
AI paper. Follow the `paper-methodology` skill's 6-step mandatory workflow strictly.

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

Execute the paper-methodology skill's 7-step mandatory workflow:

### Step 1: ANALYZE
Read all provided materials — notes, code, config, figures. Extract architecture
details, training config, dataset info. Flag any conflicts between notes and code.

### Step 2: MAP (NEW)
Generate Methodology Map:
- Extract keywords from user input (open extraction, not limited to predefined list)
- Search all reference_papers/*.txt for relevant content
- Match keywords to papers and identify narrative patterns
- Generate advisory map showing: your style grammar + relevant references + suggested structure
- The map guides subsequent steps but does not constrain technical choices

### Step 3: RECALL
Load context files before writing anything:
- Read `user_style_profile.md` for the user's writing DNA (universal grammar patterns)
- Read `error_log.md` for past corrections to avoid
- Read `memory/hard_memory.json` for confirmed term mappings and notation
- Read `map_keywords.yml` for keyword hints (advisory, not constraints)

### Step 4: PLAN
Generate the structured MethodSpec using `document_spec_template.md`. Verify the
Definition of Done for each section, including Source and Confidence fields for
all hard facts. Present for user review and STOP.

**MANDATORY GATE**: Do NOT proceed to drafting until the user explicitly confirms
with "CONFIRM", "OK", or equivalent. This gate is enforced by default unless the
user's initial prompt explicitly requests to skip confirmation (e.g., "skip review",
"generate directly", "跳过确认").

### Step 5: DRAFT
Write the Chinese methodology (plain text, full-width punctuation, no Markdown),
then the English methodology (present tense, no AI-flavored words, mirrors CN
structure). After EN generation, ask about humanizer pass.

### Step 6: AUDIT
Run the 7-pass consistency checker from `consistency_checker.md`:
terminology, numerical values, symbols/equations, structural alignment,
style compliance, error log compliance, source traceability (NEW), anti-hallucination.
Fix FAIL items in-place; add FLAG items to TODO/VERIFY.

### Step 7: ITERATE
Deliver all 4 outputs. If the user requests changes:
- Small changes (< 3 paragraphs): apply directly
- Large changes (>= 3 paragraphs or structural): produce Revision Plan first
Log any corrections to `error_log.md`. Update memory files if needed.

## Output Format

Produce all 4 outputs in sequence:
1. MethodSpec (structured, with DoD checkmarks)
2. Chinese Methodology (plain text)
3. English Methodology (plain text)
4. TODO/VERIFY List + Audit Summary
