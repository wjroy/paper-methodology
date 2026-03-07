# Style Profile (Unified)

This file is the single runtime style reference for methodology writing.
It merges the former detailed style guide and user style profile into a lean,
operational profile.

Priority rule:
1) Explicit user instruction in current session
2) hard_memory / error_log constraints
3) This style profile
4) Generic academic defaults

## 0. Calibration status (all own papers 01-05)

Rule-refinement evidence scope:
- Calibrated from all own papers: `01-own-PitGAN`, `02-own-PI-ETGCN`,
  `03-own-THGAN`, `04-own-LLM-GNN`, `05-own-TSFRA`.
- Runtime retrieval remains lightweight (top 2-3 most relevant papers), but
  global style rules below are maintained from full-scope calibration.

Major rule decisions:
- KEEP: objective subject style (`this study` / method name), present-tense
  method narration, opening framework paragraph with figure anchor, equation-role
  linkage, compact technical register, context-sensitive terminology variants.
- REVISE: opening paragraph enumeration is common but not mandatory; connector
  usage is flexible by subsection function; passive voice target should be
  preference (not hard quota).
- REMOVE: any assumption of one invariant section order or single fixed
  CN->EN term mapping across all tasks.
- CONFIRMED (post-cleaning): 05-own-TSFRA follows the same core style (objective
  subject, present tense, opening framework paragraph) but with denser equation
  chains and shorter paragraphs (50-80 words) due to its decision-centric nature.
  "Step X:" markers are characteristic of weighting-scoring-decision pattern.
- Note: Paragraph length varies by pattern type — prediction models (01-04) tend
  toward 80-120 words, decision/assessment models (05) may be 50-80 words due to
  stepwise mathematical derivations.

## 1. Structural Preferences

- Opening paragraph: one paragraph, names method, references framework figure,
  often enumerates major steps/components with numbers (1)(2)(3) or letters
  (a)(b)(c), but this is not mandatory for every architecture.
- Section planning rule: use base skeleton + selected pattern overlay from
  methodology pattern library (do not force one invariant order).
- Subsection flow: Purpose/context -> method/approach -> technical detail/formula.
- Typical subsection density: 2-4 paragraphs for technical components.

## 2. Equation Integration

- Preferred lead-ins: "is formulated as:", "can be expressed as:",
  "is defined as:".
- Always add a where block after equation placeholders.
- Preferred definition verbs: "denotes", "represents", "is defined as".
- Define symbols in first-appearance order.
- Do not present equations as isolated objects; always state their functional role
  in the current pipeline step (what the equation computes and why it is needed).

## 2.1 Logic-Explicit Technical Writing (own-paper aligned)

- Keep technical explanation compact but explicit: do not leave critical reasoning
  jumps between modules/operations.
- For each technical paragraph, explicitly cover (when supported by sources):
  1) purpose of current step/module,
  2) input to this step,
  3) operation/transformation,
  4) direct output,
  5) handoff to next step/module.
- Use local bridge clauses to show continuity (e.g., "based on the encoded input",
  "the resulting features are then fed to ..."), without tutorial-like expansion.
- Avoid module listing without functional linkage. If a module is named, also state
  its role in the pipeline and its produced artifact/state.
- For fusion/weighting/loss/constraint components, state pipeline purpose first
  (what behavior is enforced or what signal is combined) before equations/details.
- Keep explanation style precise, technical, and compact; avoid generic AI-style
  exposition, motivational filler, or over-smoothed transitions.

## 3. Voice and Tense

- Method descriptions: present tense.
- Prior published work: past tense allowed.
- English voice target: passive-leaning technical prose; do not enforce rigid
  percentage quotas.
- English subject choice: Passive voice is dominant. When active voice is needed,
  prefer "this study" / "the proposed [method]" / method name as subject.
  Avoid first-person "we" entirely.
- Chinese first-person preference: use "本文" / "本研究", avoid "我们".

## 4. Vocabulary Preferences

Preferred transitions:
- Specifically
- To [verb] ...
- As shown/illustrated in Figure X
- Accordingly

Preferred technical verbs:
- propose / present
- employ / adopt
- design
- extract

Avoid filler/promotional language:
- It is worth noting that
- Interestingly
- groundbreaking / revolutionary / unprecedented

Avoid AI-flavored words unless necessary:
- delve, tapestry, elucidate, underscore, unveil, pivotal,
  intricate, nuanced, foster, bolster, endeavor, paramount, seamless.

## 5. CN Writing Conventions

- Use full-width Chinese punctuation: ，。；：""（）
- Add spacing between Chinese and English terms/numbers when appropriate.
- Keep standard technical abbreviations in English (GAN, GCN, LLM, RMSE, MAE).
- Formal academic register; avoid colloquial expressions.

## 6. EN Writing Conventions

- No contractions.
- Avoid method-name possessives where clumsy (prefer "the output of X").
- Keep sentence rhythm varied (short + medium + long).
- Avoid overusing em-dash.

CN->EN rendering rule (upstream-aligned):
- Render technical meaning faithfully, not word-by-word literal translation.
- Keep equations, symbols, numbers, and cross-references unchanged.
- Prefer common academic vocabulary over rare decorative wording.

## 7. Cross-Reference Style

- Equation: "as defined in Equation (N)" or "as defined in Eq. (N)" (journal-dependent)
- Section: "as described in Section X.Y"
- Figure: "as illustrated in Fig. X" or "as shown in Figure X" (journal-dependent)
- Table: "as summarized in Table X"

## 7.1 Term Variant Policy (context-dependent)

- Do not force a single EN variant when own papers use multiple valid forms.
- Prefer context-dependent rendering for key terms:
  - 基坑 -> deep excavation / excavation / foundation pit
  - 围护结构 -> retaining wall / retaining structure / retaining system
  - 地表沉降 -> ground settlement
  - 风险等级 -> risk level
  - 物理约束 -> physics-informed constraint / physical constraint / mechanical prior
- Keep one variant consistent within the same subsection unless context shift
  requires another approved variant.

Chinese equivalents:
- 如公式 (N) 所示
- 如第 X.Y 节所述
- 如图 X 所示
- 如表 X 所示

## 8. Anti-Hallucination Style Guardrails

- Do not invent technical details for stylistic completeness.
- If hard facts are missing, mark [TBD]/[VERIFY] instead of guessing.
- For standard theory expansions, state basis explicitly when needed.

## 8.1 Logic-enrichment style constraints (explicit)

- Enrichment targets only supportable implicit logic gaps; it is not a generic
  verbosity increase.
- For each enriched step, prioritize this order: purpose -> transformation ->
  produced artifact/state -> handoff.
- For module/loss/fusion/constraint mentions, explain pipeline function in one
  compact sentence before or after formula reference.
- Keep own-paper style: dense technical prose, minimal rhetorical flourish,
  no tutorial-style pedagogy.

## 9. Runtime Use Checklist

Before drafting:
1) Load this profile
2) Load memory/error constraints
3) Check required terms in glossary

During drafting:
1) Keep CN-EN structure mirrored
2) Keep equation/symbol naming mirrored
3) Keep values identical across versions

After drafting:
1) Run compact audit in SKILL.md
2) Put unresolved items in TODO/VERIFY
