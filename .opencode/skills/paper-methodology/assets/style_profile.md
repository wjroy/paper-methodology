# Style Profile (Unified)

This file is the single runtime style reference for methodology writing.
It merges the former detailed style guide and user style profile into a lean,
operational profile.

Priority rule:
1) Explicit user instruction in current session
2) hard_memory / error_log constraints
3) This style profile
4) Generic academic defaults

## 1. Structural Preferences

- Opening paragraph: names method/framework; typically references framework figure
  (e.g., "As shown in Fig. X, this study develops..."); may enumerate key modules
  but does NOT always give numbered steps (only 1/5 own papers does).
- Preferred section order: Framework overview first, then module-by-module in
  pipeline order. When a physics/mechanics module exists (3/5 own papers), it
  precedes the neural architecture. This is NOT a universal invariant.
- Subsection flow: Purpose/context -> Method/approach -> Technical detail/formulation.
  This is a loose 3-beat rhythm, NOT a rigid "Motivation->Formulation->Definition".
- Typical subsection density: 2-4 paragraphs for technical components.

## 2. Equation Integration

- Preferred lead-ins: "is formulated as:", "can be expressed as:",
  "is defined as:".
- Always add a where block after equation placeholders.
- Preferred definition verbs: "denotes", "represents", "is defined as".
- Define symbols in first-appearance order.

## 3. Voice and Tense

- Method descriptions: present tense.
- Prior published work: past tense allowed.
- English voice target: about 60/40 active/passive.
- English first-person: **NONE**. All 5 own papers use zero instances of "we/our/us".
  Use "this study", "this paper", or "the proposed [model/framework]" instead.
- Chinese first-person preference: use "本文" / "本研究", avoid "我们".

## 4. Vocabulary Preferences

Dominant transition patterns (from 5 own paper statistics):
- "To [verb]..." purpose clauses (54+ instances across all papers — most frequent)
- "As shown/illustrated in Fig./Figure X" back-references (34+ instances)
- Specifically (10 instances)
- Subsequently (13 instances)
- Additionally/Moreover (11 instances, mainly Papers 01-02)
- Therefore/Thus (11 instances)
- thereby (12 instances, concentrated in Paper 04)

Low-frequency (use sparingly):
- To this end (1 instance across all 5 papers)
- In particular (1 instance across all 5 papers)
- Accordingly (2 instances across all 5 papers)

Dominant technical verbs (ranked by cross-paper frequency):
- represent, capture, model, construct, generate, compute, denote, predict,
  define, obtain, embed, integrate, adopt, employ, propose, extract, derive

Acceptable but less common:
- utilize (appears in Papers 04, 05)
- leverage (appears in Paper 04)
- design, develop, process

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
  Note: Papers 03-05 use "Fig. X"; Papers 01-02 use "Figure X". Follow target journal.
- Table: "as summarized in Table X"

Chinese equivalents:
- 如公式 (N) 所示
- 如第 X.Y 节所述
- 如图 X 所示
- 如表 X 所示

## 8. Anti-Hallucination Style Guardrails

- Do not invent technical details for stylistic completeness.
- If hard facts are missing, mark [TBD]/[VERIFY] instead of guessing.
- For standard theory expansions, state basis explicitly when needed.

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
