---
name: paper-methodology
description: >
  Generate bilingual (Chinese + English) Methodology/Methods sections for SCI papers
  in geotechnical AI. Triggers on: "写方法学", "write methodology", "methods section",
  "从脚本生成方法段", "generate methods from code", "方法学章节", "methodology chapter",
  "写 Methods", "bilingual methods". Covers ONLY Methodology/Methods (not Intro,
  Related Work, Discussion, or Abstract).
---

# paper-methodology v3.4 (pattern-library + inlined constraints)

Purpose: produce publication-ready bilingual Methodology sections with strict
anti-hallucination controls and minimal context overhead.

This version simplifies v2.x from a heavy 7-step pipeline into a compact
3-phase workflow and adds hard gate checks to prevent step skipping:

GATHER -> PLAN -> WRITE_AUDIT

Core principle: one source of truth (MethodSpec), then render CN/EN from it.

This skill supports two execution scopes under the same 3-phase workflow:
- Full-generation mode: generate a complete Methodology chapter.
- Section-level refinement mode: update only a specified section/subsection.

## 1) Non-Negotiable Rules

1. Never fabricate data, hyperparameters, metrics, baselines, or citations.
   Missing hard facts must be marked as [TBD], [VERIFY], or [CITATION NEEDED].

1.1 Citation safety rule (upstream-aligned):
- Never generate citation entries from memory.
- If a citation cannot be verified from user-provided references, keep inline
  placeholder [CITATION NEEDED] and list it in TODO/VERIFY.

2. Code/config > notes. If notes conflict with code, use code and log conflict.

3. MethodSpec-first is mandatory. Draft prose only after MethodSpec exists.

4. CN-EN alignment is mandatory: same section numbers, equations, symbols,
   figure/table references, and numerical values.

5. Output methodology prose as plain text (Word-ready, no markdown styling).

6. Domain scope: geotechnical AI only. If outside scope, explicitly decline.

7. Humanizer is ask-first. Ask user before any de-AI rewrite of EN text.

8. Section-scope safety:
- If user requests section/subsection-only update, do not default to full-chapter rewrite.
- Do not add new facts when no new source (notes/code/config) is provided.
- Do not break numbering, term mapping, equation references, or symbol consistency
  after local edits.

## 2) Runtime Assets (Read only what is needed)

Always read:
- assets/style_profile.md
- assets/error_log.md
- assets/memory/hard_memory.json
- assets/memory/soft_memory.json

Read on-demand:
- assets/methodspec_template.md (MethodSpec skeleton with traceability fields)
- assets/term_glossary.yml (term checks / CN-EN mapping)
- assets/notation.md (symbol/notation checks)
- assets/methodology_patterns.yml (pattern library for PLAN selection)
- assets/methodology_outline.md (base skeleton + pattern overlays)
- assets/reference_papers/*.txt (only top relevant files)

Do not load all reference papers by default. Use selective retrieval.

## 3) 3-Phase Workflow

### Phase A: GATHER

Goal: collect facts and constraints before writing.

A1. Parse user input + code/config/notes and extract:
- Problem + engineering context
- Inputs/outputs
- Model components
- Loss definitions
- Training setup (if provided)
- Metrics + baselines
- Figure/table anchors (if provided)

A2. Detect conflicts (notes vs code/config) and gaps (missing hard facts).

A2.1 Required hard-fact set (for drafting safety):
- Task objective (what to predict/classify/estimate)
- At least one model identifier (framework name or component names)
- At least one input/output definition
- At least one training/evaluation anchor (loss or metric)

If any item in this set is missing and cannot be inferred safely, trigger
Clarification Block before moving to PLAN.

A3. Build a lightweight Methodology Map:
- Detect keywords from user content (open extraction, no rigid dictionary needed)
- Retrieve only top 3-5 relevant reference papers
- Learn structure logic only (never copy values/content)

A4. Trigger user-question node when needed:
- If required hard facts are missing and cannot be inferred safely,
  ask one compact Clarification Block.
- Clarification Block format:
  1) Missing hard facts list
  2) Recommended default handling ([TBD] or move to Case Study)
  3) What changes if user confirms/provides values

Hard rule: If Clarification Block is triggered, do not enter Phase B until user
replies or user explicitly asks to proceed with placeholders.

### Phase B: PLAN (MethodSpec gate)

Goal: create a single source of truth for CN and EN drafting.

B0. Select methodology pattern before writing MethodSpec.
- Match current task to one primary pattern from assets/methodology_patterns.yml.
- Record short rationale and 1-2 fallback patterns.
- Pattern selection is adaptive: when new paper's technical architecture differs
  from own papers, select the most suitable pattern or use hybrid patterns.
  Do not default to a single pattern.
- Never force a single invariant order across all own papers.

B1. Build section plan from base skeleton + selected pattern overlay.
- Use assets/methodology_outline.md as base skeleton.
- Apply selected pattern overlay to adjust ordering/emphasis.
- Keep module flow consistent with user notes and code/config.

B2. Produce MethodSpec with these sections:
1. Metadata
2. Problem definition
3. Framework overview
4. Physical/mechanical model (or N/A)
5. Data
6. Architecture
7. Loss function
8. Training config (default: moved to Case Study)
9. Evaluation metrics
10. Conflicts and gaps

B3. For each hard-fact field in Sections 2-9 of the MethodSpec, include:
- Source: specific origin (e.g. "user notes", "@train.py#L42",
  "@config.yaml#L3", "hard_memory.json"). Use [TBD] if unknown.
- Confidence: OK or NEEDS_VERIFY
See assets/methodspec_template.md for the full field-by-field layout.

B4. Present MethodSpec and enforce confirmation gate.
Proceed only if user replies equivalent to CONFIRM/OK/proceed.

Hard rule: No CN/EN drafting is allowed before this gate is satisfied, except
when explicit skip-gate exception is present in user instruction.

Skip-gate exception only when user explicitly says:
- skip confirmation / 跳过确认
- generate directly / 直接生成
- no review needed / 无需审核

### Phase C: WRITE_AUDIT

Goal: draft CN and EN from MethodSpec, then run compact audit.

C1. Draft Chinese Methodology
- Follow style_profile
- Dense paragraphs, formal register
- Full-width Chinese punctuation
- Keep standard technical terms in English where appropriate (GAN, GCN, etc.)
- Equation placeholders: [公式 (N): ...]

C2. Draft English Methodology
- Mirror CN structure exactly
- Present tense for method description
- Prefer objective subject style from style_profile (typically "this study" / "this paper")
- Equation placeholders: [Equation (N): ...]

C3. Ask humanizer question (do not auto-apply)
- "English version is ready. Apply de-AI humanizer pass?"
- If user agrees, apply inlined de-AI constraints:
  1) Keep all technical content unchanged (numbers/formulas/symbols/refs)
  2) Remove filler/promotional/mechanical connectors
  3) Preserve passive-dominant voice and technical precision characteristic
     of own papers
  4) Keep text if already natural (return pass verdict)

C3.1 Optional refinement operations (ask-first, never auto-apply):
- Expand: +5 to +15 words, add only logic-explicit details implied by source.
- Compress: -5 to -15 words, keep all technical facts unchanged.
- Polish: improve clarity/grammar/formality, keep terminology and references fixed.

All refinement operations require explicit user confirmation before execution.

C3.2 Minimal logic/redline check (before delivery)
- Check only critical issues: contradictions, core term inconsistency,
  severe grammar blocking comprehension, and logic discontinuities that block
  technical understanding.
- Catch step jumps where a required intermediate operation is omitted in prose
  (A -> C with no supportable B explanation).
- Catch functionless module mentions (module named but role/output in pipeline
  is unclear).
- Catch formulas introduced without role/handoff explanation.
- Catch fusion/weighting/loss/constraint mentions that state names only but do
  not state pipeline purpose.
- Do not report style-only issues in this pass.
- Keep this check lightweight and repair-oriented (no verbose reviewer critique).

C3.3 Logic-enrichment pass (inlined, targeted; before audit)
- Purpose: make supportable implicit technical reasoning explicit and improve
  local continuity between steps/modules.
- This is NOT generic expansion and NOT a style rewrite.
- Operate only on logic gaps detected in C3.2 and only when evidence exists in
  MethodSpec and/or user-provided notes/code/config.
- Allowed enrichments:
  1) Add purpose sentence for a module/step,
  2) Add compact input -> operation -> output statement,
  3) Add explicit handoff clause to the next step/subsection,
  4) Add one-line equation/module role explanation tied to pipeline function.
- Hard constraints:
  - No new facts, parameters, citations, modules, or results.
  - Keep all values/symbols/references unchanged.
  - Preserve own-paper style: precise, technical, compact, non-tutorial.
  - If source support is insufficient, keep original text and add TODO/VERIFY
    rather than guessing.

### Section-level refinement mode (overlay; keep 3-phase workflow)

Trigger this mode when user explicitly requests local refinement and provides:
- Target section/subsection identifier (e.g., 3.2, 3.2.1, "Loss Function")
- Existing section text (CN, EN, or both)
- Added notes and/or added code/config paths
- Operation type: expand | rewrite | correct | bilingual-sync

R1. Scope lock:
- Treat this as local update, not chapter rewrite.
- Preserve all non-target sections by default.

R2. Phase A behavior in local mode:
- Extract only target-related facts from newly added sources.
- Re-check conflicts by code/config > notes for target-related facts only.
- Keep unchanged facts untouched.

R3. Phase B behavior in local mode (MethodSpec-first still mandatory):
- Update only MethodSpec hard-fact fields linked to the target section/subsection.
- Keep non-target MethodSpec fields unchanged unless a dependency is required for
  consistency (term/symbol/numbering/cross-reference).
- For every updated hard-fact field, refresh Source and Confidence.

R4. Phase C behavior in local mode:
- Rewrite/expand only the target CN/EN section/subsection.
- Keep all other sections unchanged by default.

R5. Allowed linked edits outside target scope (minimal only):
- Term normalization required by glossary mapping
- Symbol/equation numbering and cross-reference repair
- One-hop context bridge sentence when target paragraph no longer connects
  logically to adjacent text

R6. Alignment rules after local update:
- CN and EN must stay section-aligned for the updated scope.
- Terms, symbols, equation indices, figure/table references, and numeric values
  must match across CN/EN.

R7. Explicit prohibitions in local mode:
- No full-chapter rewrite unless user explicitly requests it.
- No unsourced detail injection when added sources do not support it.
- No local edit that leaves global numbering/notation/cross-references broken.

C4. Compact 6-pass audit (must run before delivery)
1. Terminology consistency (glossary + hard_memory)
2. Numerical consistency (MethodSpec vs CN vs EN)
3. Equation/symbol consistency (notation + where blocks)
4. Structural alignment (CN vs EN)
5. Error-log compliance (no repeated mistakes)
6. Traceability — for every hard-fact field in MethodSpec Sections 2-9:
   a. Source is populated (not blank). Blank Source = FAIL.
   b. Confidence is populated (OK or NEEDS_VERIFY). Blank = FAIL.
   c. Every Source: [TBD] has a matching entry in Section 10 and TODO/VERIFY.
   d. Every value in CN/EN prose is traceable back to the MethodSpec field
        that sourced it. Unsourced value in prose = FAIL.

C4.2 Lightweight logic continuity check (post-enrichment, mandatory):
- Verify no unresolved step jumps remain in key pipeline descriptions.
- Verify each newly mentioned module has a stated functional role and output.
- Verify each equation/loss/fusion/constraint mention includes purpose or handoff.
- Verify fixes remain source-grounded (no unsourced inserted value/module/result).
- Report only PASS/FLAG/FAIL with short repair notes.

C4.1 Additional checks for section-level refinement mode:
- Scope integrity: only target section/subsection changed, except allowed minimal
  linked edits.
- Terminology/notation/numbering integrity after local update.
- CN/EN synchronization for updated scope.
- No unsourced value introduced by local edit.

Fix FAIL items before delivery. Put unresolved items in TODO/VERIFY.

C5. Pre-delivery gate checklist (mandatory):
- Gate G1: Phase A completed (facts, gaps, conflict scan)
- Gate G2: MethodSpec produced
- Gate G3: Confirmation satisfied OR explicit skip-gate instruction found
- Gate G4: CN and EN drafted from the same MethodSpec
- Gate G5: 6-pass audit executed

If any gate is false, stop and repair before final output.

## 4) MethodSpec Template

Use the full template in: assets/methodspec_template.md

Key structural rules (also embedded in the template file):
- 10 sections: Metadata, Problem Definition, Framework Overview,
  Physical/Mechanical Model, Data, Architecture, Loss Function,
  Training Configuration, Evaluation Metrics, Conflicts and Gaps.
- Every hard-fact field in Sections 2-9 MUST carry:
    Source:      origin of the fact (e.g. "user notes", "@config.yaml#L3", "[TBD]")
    Confidence:  OK | NEEDS_VERIFY
- If Source cannot be determined, write Source: [TBD], Confidence: NEEDS_VERIFY,
  and add a matching entry in Section 10.
- Blank Source on any hard-fact field = Audit Pass 6 (Traceability) FAIL.
- Section 8 (Training Config) defaults to [MOVED TO CASE STUDY] unless user
  explicitly requests methodology-level detail.

## 5) Output Contract

Deliver in this order:
1. MethodSpec
2. Chinese Methodology
3. English Methodology
4. TODO/VERIFY + Audit summary

If placeholders are used, TODO/VERIFY must explicitly list user actions needed
to replace each placeholder.

Audit summary format:

CONSISTENCY AUDIT SUMMARY
=========================
Terminology: PASS/FLAG/FAIL
Numerical: PASS/FLAG/FAIL
Equation/Symbol: PASS/FLAG/FAIL
Structure: PASS/FLAG/FAIL
Error-log: PASS/FLAG/FAIL
Traceability: PASS/FLAG/FAIL

## 6) Revision Policy

Small revision (<3 paragraphs, no structure change): revise directly.

Section-level refinement (default local update):
- If user requests a target section/subsection update, perform local revision by
  default and keep non-target sections unchanged.
- If newly added facts force chapter-level structure changes (global renumbering,
  reordered major modules, cross-section dependency expansion), escalate to Large
  revision and present Revision Plan first.

Large revision (>=3 paragraphs or structure/numbering/equation changes):
present a Revision Plan first, then wait for user approval.

Revision Plan format:

REVISION PLAN
=============
Trigger: ...
Changes:
1. ...
2. ...
Preserved:
- ...
Alignment impact:
- ...
Risks:
- ...

## 7) Pruning and Generalization Notes

- Prefer universal method grammar over paper-specific imitation.
- Reference papers are for structure logic, not content copying.
- If own papers are unavailable, still run full workflow using user inputs,
  memory assets, and domain conventions.
- Keep prompts compact; avoid loading non-essential assets.
- Use inlined constraints in this file for rendering/humanizer/refinement/
  logic-redline checks; avoid separate prompt-pack dependency.

## 8) Runtime Efficiency Rules

- Prefer targeted lookup over full-file loading for large assets.
- For `term_glossary.yml`, retrieve only terms used in current draft domain.
- For reference papers, retrieve top 3-5 by relevance only.
- Do not mirror specific wording from any reference paper.

## 9) Default Clarification Templates

Use one of these when question node is triggered.

Template A (missing hard facts):
1) Missing facts: ...
2) Recommended default: keep as [TBD] / move detail to Case Study
3) Impact: if provided now, MethodSpec + both language drafts will be updated

Template B (conflict found):
1) Conflict: notes say X, code/config says Y
2) Default policy: use Y (code/config wins)
3) Please confirm whether to override with explicit instruction

## 10) Upstream Alignment (external repos)

This skill explicitly incorporates writing constraints from:
- https://github.com/Leey21/awesome-ai-research-writing
- https://github.com/Orchestra-Research/AI-Research-SKILLs/tree/main/20-ml-paper-writing

Adopted principles:
- Keep output plain and Word-friendly (no markdown styling in methodology text).
- Prefer natural paragraph flow over list-heavy output in final prose.
- Avoid AI-flavored filler and promotional language.
- Use present tense for method description by default.
- Be proactive in drafting, but enforce hard gates to prevent step skipping.
- Treat citation reliability as critical: unverifiable references must remain
  explicit placeholders instead of guessed entries.

Scope note:
- This skill remains Methodology-only (bilingual CN+EN for geotechnical AI),
  while inheriting the above writing and citation safety practices.
