---
name: paper-methodology
description: >
  Generate bilingual (Chinese + English) Methodology/Methods sections for SCI papers
  in geotechnical AI. Triggers on: "写方法学", "write methodology", "methods section",
  "从脚本生成方法段", "generate methods from code", "方法学章节", "methodology chapter",
  "写 Methods", "bilingual methods". Explicitly excludes Introduction, Discussion,
  Related Work, and Abstract — this skill covers ONLY the Methodology/Methods section.
---

# paper-methodology v2.0

Generate publication-ready bilingual Methodology sections for SCI papers in the
geotechnical AI domain (excavation, tunnelling, foundation, underground construction
+ deep learning, GNN, GAN, LLM, physics-informed models).

**Version 2.0 changes**: 6-step mandatory workflow (Analyze → Recall → Plan →
Draft → Audit → Iterate), persistent style profile, error memory, hard/soft
memory system, Definition of Done enforcement, Revision Plan protocol, and
dedicated consistency checker.

---

## NON-NEGOTIABLE RULES

These rules override everything else. Violation of any rule invalidates the output.

1. **NEVER fabricate** datasets, parameters, hyperparameters, baselines, metrics,
   numerical results, or citations. If information is missing, insert `[TODO: ...]`
   or `[CITATION NEEDED]`.

2. **Code/config wins over notes.** If the user's written notes say batch_size=64
   but their config file says batch_size=32, use 32 and flag the conflict in
   TODO/VERIFY.

3. **MethodSpec first, then render.** Always produce the structured MethodSpec
   before writing either language version. Never skip this step.

4. **CN-EN alignment is mandatory.** Both versions must have identical section
   structure, equation numbering, figure/table references, symbol usage, and
   numerical values.

5. **Plain text output only.** Output is Word-ready. No Markdown formatting
   (no bold, italic, headings, bullets). No LaTeX. Section headers as plain
   numbered text (e.g., "3.1 Overall Framework").

6. **Humanizer is ask-first.** After generating EN, ask the user: "Would you like
   me to apply a de-AI pass to the English version?" Do not apply automatically.

7. **Present tense for methods.** Past tense only when citing prior published work.

8. **Domain scope: geotechnical AI only.** Do not generalize to other domains.
   If the user's work falls outside this scope, inform them and decline.

9. **Read before writing.** Before generating ANY text, you MUST complete the
   ANALYZE and RECALL steps. Never draft without first reading the style profile,
   error log, and memory files.

10. **Revision Plan for large changes.** Any modification affecting 3+ paragraphs
    or changing section structure requires a Revision Plan (see
    `document_spec_template.md`) approved by the user before execution.

---

## INPUT SPECIFICATION

The user should provide some combination of:

### Required (at least one)
- **Research notes / outline** in Chinese or English (can be rough, bullet-point)
- **Code repository** path or key scripts (model definition, training script, config)
- **Figures** of the architecture or framework

### Optional (improves output quality)
- Target journal or conference name
- Draft of other sections (Abstract, Introduction) for context
- Specific equation derivations
- Parameter tables
- Published reference papers for style matching

---

## 6-STEP MANDATORY WORKFLOW

Every invocation of this skill follows this exact sequence. No step may be skipped.

```
ANALYZE → RECALL → PLAN → DRAFT → AUDIT → ITERATE
```

### Step 1: ANALYZE — Read All Materials

**Purpose**: Gather all facts from user input before writing anything.

**Actions**:
1. Read ALL provided code/config files completely.
2. Read ALL provided notes/outlines.
3. Read ALL referenced figures (describe what you see).
4. Extract into working memory:
   - Problem definition and physical context
   - Model architecture (layers, dimensions, activations)
   - Training configuration (optimizer, lr, batch_size, epochs, scheduler)
   - Dataset description (source, size, features, split ratio)
   - Loss function formulation
   - Evaluation metrics
   - Baseline methods mentioned
   - Any citations referenced
5. **Conflict detection**: Compare notes vs. code/config. Log every discrepancy
   with both values.

**Gate**: Do not proceed until all provided materials have been read. If
materials are incomplete, list what is missing and ask the user.

### Step 2: MAP — Generate Methodology Map

**Purpose**: Analyze research direction, extract keywords, and generate personalized methodology map from reference papers.

**Actions**:

1. **Open keyword extraction**:
   - Parse user's research description for technical terms
   - Identify model names (LLM, TSFM, GNN, etc.)
   - Identify methods (LoRA, GAN, etc.)
   - Identify application domain (excavation, tunnel, etc.)
   - Ask clarifying questions for ambiguous terms

2. **Search reference papers** (all 18 txt files):
   - Search for extracted keywords in all reference_papers/*.txt
   - Calculate relevance scores based on keyword matches
   - Prioritize: exact matches > variant matches > semantic proximity
   - Return top 5-7 most relevant papers

3. **Generate Methodology Map**:
   ```
   METHODOLOGY MAP (Auto-generated)
   ════════════════════════════════════════════════════════════
   
   Detected Keywords: [list of identified keywords]
   
   Your Style Profile (Universal Grammar):
   - Component introduction: "[Component] serves as [role]"
   - Function description: "transforms [input] into [output] for [purpose]"
   - Overview format: 3-4 numbered steps
   - Section order: Physics/Data → Model
   - Paragraph flow: Motivation → Formulation → Definition
   
   Reference Papers (by relevance):
   1. [FileName.txt] (Score: X.XX)
      └─ Learn: [What narrative structure to learn from this paper]
      └─ Not: [What NOT to copy - specific values/content]
   
   2. [FileName.txt] (Score: X.XX)
      └─ Learn: [...]
      └─ Not: [...]
   
   Suggested Structure (based on your style):
   - Section X.1: Overview (your 3-4 step pattern)
   - Section X.2: [Component/Model 1] (reference [paper] for structure)
   - Section X.3: [Component/Model 2] (reference [paper] for structure)
   - ...
   
   ⚠️  CRITICAL RULES:
   1. Use reference papers ONLY for narrative STRUCTURE and LOGIC
   2. ALL specific values/params/content must be YOURS from code/experiments
   3. Write using YOUR style grammar (from user_style_profile.md)
   4. Adapt technical descriptions to YOUR specific implementation
   
   ════════════════════════════════════════════════════════════
   ```

**Gate**: The Map is advisory. Proceed to Step 3 with the map in context.

### Step 3: RECALL — Load Memory & Context

**Purpose**: Load the user's established patterns and past corrections before writing.

**Actions** (read these files in order):
1. **Read `user_style_profile.md`** — Load the user's writing DNA:
   - Opening paragraph pattern
   - Section ordering preference (physics-first)
   - Equation integration style
   - Voice and tense patterns
   - Vocabulary preferences
   - Paragraph architecture rules
   - Chinese-specific conventions
2. **Read `error_log.md`** — Load past corrections:
   - Identify all logged error patterns
   - Internalize each correction as a negative constraint
   - Flag any that are relevant to the current paper
3. **Read `memory/hard_memory.json`** — Load exact facts:
   - Critical term mappings (CN-EN)
   - Standard units
   - Notation conventions
   - Journal formatting rules (if target journal is specified)
4. **Read `memory/soft_memory.json`** — Load style preferences:
   - Paragraph preferences
   - Voice preferences
   - Connector preferences
   - Equation preferences
   - Cross-reference formats

**Gate**: Confirm internally that all 4 files were read. If any file is missing
or empty, note it and proceed with defaults from `style_guide_methodology.md`.

### Step 4: PLAN — Generate MethodSpec with DoD

**Purpose**: Create the single source of truth before any prose is written.

**Actions**:
1. Fill in the MethodSpec template from `document_spec_template.md`.
2. For each section, verify the Definition of Done (DoD) checklist.
3. Mark any DoD item that cannot be satisfied as `[TBD]`.
4. Determine the section hierarchy based on paper type:
   - Surrogate model → physics model first (per `methodology_outline.md`)
   - Spatiotemporal prediction → graph construction as dedicated subsection
   - LLM-enhanced → LLM integration point as dedicated subsection
   - Risk assessment → indicator system first
5. Compile the CONFLICTS & GAPS section.
6. **Present MethodSpec to the user** and STOP for confirmation:

   "MethodSpec is ready for review. Please check:
   1. Are all values correct? (Especially Section 8: Training Configuration)
   2. Are all Source fields populated for hard facts?
   3. Are there any missing components not captured above?
   4. Reply CONFIRM or OK to proceed to DRAFT, or provide corrections."

**Gate (MANDATORY)**: Do NOT proceed to DRAFT until the user explicitly replies with
"CONFIRM", "OK", "proceed", or equivalent affirmative response. This gate is ALWAYS
enforced UNLESS the user's initial prompt explicitly includes phrases like:
- "skip confirmation" / "跳过确认"
- "generate directly" / "直接生成"
- "no review needed" / "无需审核"

If the user provides corrections:
- Update the MethodSpec with corrected values
- Update Source fields if corrections reveal new sources
- Log corrections in `error_log.md` if they represent a generalizable mistake
- Re-present the updated MethodSpec and wait for confirmation again

**Exception: Skip-confirmation mode**

If the user's initial prompt contains explicit skip-confirmation instructions
(e.g., "write methodology, skip MethodSpec confirmation" or "直接生成，无需确认"),
the AI may proceed directly from PLAN to DRAFT without waiting. However, the
MethodSpec must still be generated and included in the final output.

### Step 4: DRAFT — Write CN and EN Methodology

**Purpose**: Produce both language versions from the confirmed MethodSpec.

#### Step 4a: Chinese Methodology (CN)

Write the Chinese methodology section following these rules:

**Structure**: Follow `methodology_outline.md` hierarchy, adapted per MethodSpec.

**Style rules** (from `style_guide_methodology.md` + `user_style_profile.md`):
- Dense continuous paragraphs, 100-250 words each, one core idea per paragraph
- Full-width Chinese punctuation throughout: ，。；：""（）
- Space between Chinese characters and English terms: "采用 GAN 模型"
- Keep standard English terms in English: Transformer, GAN, GCN, LSTM, attention
- No oral expressions: use "实验结果表明" not "我们发现"
- Use "本文" / "本研究" instead of "我们"
- Equation placeholders: "[公式 (N): brief description]"
- "where" blocks after equations: "其中，X 表示...，Y 代表..."
- Reference figures/tables before they appear: "如图 X 所示"
- Define abbreviations on first use: "生成对抗网络 (GAN)"

**Opening paragraph pattern** (from style profile, HIGH confidence):
"本研究提出的 [METHOD] 框架主要包含以下几个步骤：（1）...；（2）...；
（3）...。图 X 展示了该方法的总体框架。"

**Terminology**: Use `term_glossary.yml` CN column. Cross-check against
`memory/hard_memory.json` critical_terms.

**Symbols**: Use `notation.md` conventions.

#### Step 4b: English Methodology (EN)

Write the English methodology section following these rules:

**Structure**: Must mirror the CN version exactly — same sections, same order,
same equation numbers, same figure/table references.

**Style rules** (from `style_guide_methodology.md` + `user_style_profile.md`):
- Dense continuous paragraphs, no bullet lists
- Present tense for method description
- ~60/40 active/passive voice ratio (from style profile)
- Moderate use of "we" (5-10 times per methodology section)
- No contractions ("does not" not "doesn't")
- No possessive for method names ("the output of PitGAN" not "PitGAN's output")
- Equation placeholders: "[Equation (N): brief description]"
- "where" blocks: "where X denotes ..., Y represents ..."
- Reference figures/tables before they appear: "as shown in Figure X"
- Define abbreviations on first use: "generative adversarial network (GAN)"

**Opening paragraph pattern** (from style profile, HIGH confidence):
"The proposed [METHOD] framework consists of [N] main components: (1) ...,
(2) ..., and (3) .... The overall architecture is illustrated in Figure X."

**Anti-AI writing rules** (from `style_guide_methodology.md` Section 6):
- Avoid these words unless technically necessary: leverage, delve, tapestry,
  utilize, elucidate, underscore, unveil, pivotal, intricate, nuanced, foster,
  bolster, endeavor, paramount, comprehensive, robust, seamless, cutting-edge
- Minimal em-dash usage; prefer commas or subordinate clauses
- No significance inflation without statistical backing
- No promotional language (groundbreaking, revolutionary, unprecedented)
- No filler phrases (It is worth noting that, Interestingly)
- Vary sentence rhythm — mix short and long sentences

**Terminology**: Use `term_glossary.yml` EN column. Cross-check against
`memory/hard_memory.json` critical_terms.

**Preferred vocabulary** (from style profile, HIGH confidence):
- Transition phrases: "Specifically", "To this end", "In particular"
- Technical verbs: "propose" / "present", "employ" / "adopt", "design", "extract"
- Equation introduction: "is formulated as:", "can be expressed as:"
- Cross-references: "as defined in Equation (N)", "as described in Section X.Y"

#### Step 4c: Optional Humanizer Pass (Ask First)

After generating EN, ask the user:
> "The English methodology section is ready. Would you like me to apply a
> de-AI humanizer pass to make the writing style more natural?"

**If user says yes**, apply these transformations:

1. **Scan for AI patterns** (from humanizer skill):
   - Significance inflation ("significantly", "substantially" without evidence)
   - -ing phrase proliferation ("Leveraging the power of...")
   - Promotional language
   - Vague attribution ("Research shows that...")
   - Em-dash overuse
   - Rule-of-three lists
   - Synonym cycling (varying words for the same concept)
   - Filler phrases

2. **Rewrite** to address found patterns while preserving:
   - ALL technical terms, model names, abbreviations (NEVER change these)
   - ALL numerical values, parameters, hyperparameters
   - ALL equation blocks and "where" definitions
   - ALL figure/table references
   - The overall meaning and technical accuracy

3. **Add natural rhythm**:
   - Vary sentence length (some short declarative, some longer compound)
   - Occasional first-person where natural ("We design..." vs "is designed...")
   - Specific rather than vague language

4. **Verify preservation**: After humanizing, re-run Pass 2 (Numerical Value Audit)
   of the consistency checker to confirm no technical content was altered.

### Step 5: AUDIT — Run Consistency Checker

**Purpose**: Systematic verification of the generated text before delivery.

**Actions**: Execute all 7 audit passes from `consistency_checker.md`:

1. **Terminology Consistency Audit** — terms match glossary and hard_memory
2. **Numerical Value Audit** — all numbers match MethodSpec, CN, and EN
3. **Symbol & Equation Audit** — equations aligned, symbols defined
4. **Structural Alignment Audit** — CN-EN section structure matches
5. **Style Profile Compliance Audit** — output matches user_style_profile.md
6. **Error Log Compliance Audit** — no past mistakes repeated
7. **Anti-Hallucination Audit** — all values traceable to user input

**For FAIL items**: Fix in-place. Update both CN and EN versions as needed.
**For FLAG items**: Add to TODO/VERIFY list.

**Compile audit summary** (template in consistency_checker.md).

### Step 6: ITERATE — Deliver & Handle Revisions

**Purpose**: Present final output and manage user feedback.

**Actions**:
1. Deliver the 4 outputs in sequence:
   - **Output 1**: MethodSpec (structured)
   - **Output 2**: Chinese Methodology (plain text)
   - **Output 3**: English Methodology (plain text)
   - **Output 4**: TODO/VERIFY List (with audit summary)

2. If the user requests changes:
   - **Small change** (< 3 paragraphs, no structural change): Apply directly.
   - **Large change** (>= 3 paragraphs or structural): Produce a Revision Plan
     (format in `document_spec_template.md`) and wait for user approval.
   - After applying changes, re-run relevant audit passes.
   - Log any corrections that represent generalizable mistakes in `error_log.md`.

3. Update memory files if the session revealed new patterns:
   - New confirmed term mappings → `memory/hard_memory.json`
   - New style preferences → `memory/soft_memory.json`

---

## SECTION HIERARCHY GUIDE

Refer to `assets/methodology_outline.md` for the full flexible template.

**Key principle**: The hierarchy is a guideline, not a rigid template. Adapt based
on the paper's content. The invariant pattern is:

1. Overview paragraph with numbered steps
2. Physics/mechanical model (if applicable)
3. Data generation/processing
4. Model architecture (with sub-subsections per component)
5. Loss function and training
6. Evaluation metrics (may go in Experiments instead)

---

## WRITING STYLE REFERENCE

Refer to `assets/style_guide_methodology.md` for detailed rules covering:
- Prose structure and paragraph conventions
- Tense and voice rules
- Terminology discipline
- Equation conventions
- Figure/table protocol
- Anti-AI writing patterns (with 20+ word substitution table)
- Chinese-specific style rules
- Cross-reference patterns
- Output format rules for Word compatibility

The user's personal style patterns are in `assets/user_style_profile.md`.
When in conflict, `user_style_profile.md` takes precedence over the general
`style_guide_methodology.md`.

---

## TERMINOLOGY & NOTATION

- **Term glossary**: `assets/term_glossary.yml` — CN-EN mapping for 200+ terms
  across geotechnical engineering, neural networks, GAN, GNN, attention/Transformer,
  LLM, spatiotemporal modeling, training/evaluation, data processing, statistical ML,
  and physics-informed methods.

- **Notation conventions**: `assets/notation.md` — subscript system, common symbols
  (geotechnical parameters, NN symbols, GAN symbols, evaluation metrics), and
  notation rules (matrices, vectors, scalars, indexing).

- **Hard memory terms**: `assets/memory/hard_memory.json` — user-confirmed exact
  term mappings that override the general glossary.

---

## ANTI-HALLUCINATION PROTOCOL

### Hard constraints
1. Every dataset name must come from the user's input.
2. Every hyperparameter value must come from code/config or be marked `[TBD]`.
3. Every baseline model name must come from the user's input.
4. Every metric value must come from experimental results provided by the user.
5. Every citation must be user-provided or marked `[CITATION NEEDED]`.
   **Never generate a BibTeX entry or reference string from memory** — AI-generated
   citations have ~40% error rate (per ml-paper-writing SKILL).

### Soft constraints (flag but don't block)
6. If the user claims a result but provides no evidence, include it but add
   `[VERIFY: no supporting data provided]`.
7. If a standard technique is mentioned without details (e.g., "we use Adam"),
   it is acceptable to include standard descriptions but flag non-standard
   claims about the technique.

### Conflict resolution
8. Code/config always wins over notes.
9. Published paper always wins over draft notes.
10. User's explicit instruction always wins over skill defaults.

---

## CN-EN TRANSLATION QUALITY RULES

Adapted from awesome-ai-research-writing CN-to-EN prompt:

### For CN -> EN rendering (not literal translation)
- Render the same technical content in natural English academic prose
- Do not translate word-by-word; restructure sentences for English flow
- Keep the same level of technical detail
- Present tense for methods, past tense only for prior work citations
- Use common words; avoid obscure vocabulary
- No bold, italic, or em-dashes in output

### For ensuring CN-EN consistency
- Both versions generated from the same MethodSpec (single source of truth)
- Section numbering must match exactly
- Equation numbering must match exactly
- All numerical values must be identical
- All symbol definitions must be identical
- All figure/table references must correspond

---

## LOGIC CHECK INTEGRATION

Integrated into the AUDIT step (Step 5). After completing both versions,
the consistency checker's 7 passes cover:

1. Are there contradictory claims between sections?
2. Does any technical term change names mid-text without explanation?
3. Are there sentences that are ambiguous or could be misread?
4. Are equation variables used before being defined?

If all pass: proceed to output.
If any fail: fix the issue and note it in the audit summary.

---

## PERSISTENT LEARNING SYSTEM

This skill improves over time through 3 mechanisms:

### 1. Error Log (`error_log.md`)
- Every user correction is logged as a "negative constraint"
- The AI reads ALL logged errors during the RECALL step
- Prevents the same mistake from recurring across sessions
- Categories: TERMINOLOGY, FORMATTING, STYLE, FACTUAL, STRUCTURAL, TRANSLATION

### 2. Hard Memory (`memory/hard_memory.json`)
- Stores confirmed facts: term mappings, units, notation, journal rules
- The AI treats these as ground truth during generation
- Updated when the user confirms a new term or convention

### 3. Soft Memory (`memory/soft_memory.json`)
- Stores style preferences: paragraph length, voice ratio, connector usage
- Influences style choices but can be overridden by explicit instructions
- Updated when consistent new preferences are observed

### Updating Memory Files
After a session where corrections were made:
1. Append correction entries to `error_log.md` using the template format
2. If a correction reveals a new confirmed fact, add to `hard_memory.json`
3. If a correction reveals a new preference, add to `soft_memory.json`

---

## STYLE TRANSFER SYSTEM

### Initial Setup (run once)
Use `style_extractor.md` to analyze the user's published papers and populate
`user_style_profile.md`. This has been pre-populated from analysis of 3 papers
(PitGAN, PI-ETGCN, THGAN).

### Ongoing Use
- The AI reads `user_style_profile.md` during every RECALL step
- The profile acts as a "Style DNA" — the AI mimics the user's established
  writing patterns rather than generic academic style
- HIGH confidence patterns are mandatory; MEDIUM are strongly preferred;
  LOW are optional guidelines

### Updating the Style Profile
When the user publishes a new paper:
1. Add the methodology section to `reference_papers/` as `NN-own-[NAME].txt`
2. Run `style_extractor.md` on the updated paper set
3. Merge new findings into `user_style_profile.md`

---

## COMPLETE OUTPUT FORMAT

The skill produces 4 sequential outputs:

### Output 1: MethodSpec
```
METHODSPEC v2.0
===============
[Structured MethodSpec with DoD checkmarks — see document_spec_template.md]
```

### Output 2: Chinese Methodology
```
X. 方法 / 研究方法

X.1 总体框架
[Dense paragraphs, plain text, full-width punctuation...]

X.2 [Next subsection]
[...]
```

### Output 3: English Methodology
```
X. Methodology / Methods

X.1 Overall Framework
[Dense paragraphs, plain text, no Markdown...]

X.2 [Next subsection]
[...]
```

### Output 4: TODO/VERIFY List + Audit Summary
```
CONSISTENCY AUDIT SUMMARY
=========================
[7-pass audit results — see consistency_checker.md]

TODO/VERIFY LIST
================
[TODO] Item description — what the user needs to provide
[VERIFY] Item description — what the user needs to confirm
[CONFLICT] Notes say X, code says Y — using Y (code wins)
[CITATION NEEDED] Reference for claim about ...
```

---

## REFERENCE ASSETS

All assets are in `assets/` relative to this SKILL.md:

| File | Purpose |
|------|---------|
| `reference_papers/README.md` | Index of 9 source papers with naming convention |
| `reference_papers/01-own-*.txt` through `09-other-*.txt` | Full text of reference papers |
| `methodology_outline.md` | Flexible section hierarchy template |
| `style_guide_methodology.md` | Comprehensive writing style rules |
| `term_glossary.yml` | CN-EN term mapping (200+ entries across 10 categories) |
| `notation.md` | Symbol and subscript conventions |
| `checklist.md` | Legacy post-generation checklist (superseded by consistency_checker.md) |
| `style_extractor.md` | Prompt to extract user's Style DNA from their papers |
| `user_style_profile.md` | User's personal writing patterns (pre-populated) |
| `error_log.md` | Persistent error memory — grows over time |
| `memory/hard_memory.json` | Domain-specific exact facts (terms, units, notation) |
| `memory/soft_memory.json` | Domain-specific preferences (style, voice, connectors) |
| `document_spec_template.md` | MethodSpec template with DoD + Revision Plan protocol |
| `consistency_checker.md` | 7-pass consistency audit procedure |
