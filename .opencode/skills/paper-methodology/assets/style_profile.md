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

- Opening paragraph: one paragraph, names method, gives 3-4 numbered steps,
  references framework figure.
- Preferred section order: Overview -> Physics/Mechanics (if any) -> Data ->
  Architecture -> Loss/Training -> Metrics.
- Subsection flow: Motivation -> Formulation -> Definition.
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
- English first-person: moderate and controlled (e.g., 5-10 uses in long method).
- Chinese first-person preference: use "本文" / "本研究", avoid "我们".

## 4. Vocabulary Preferences

Preferred transitions:
- Specifically
- To this end
- In particular
- Accordingly
- As illustrated in Figure X

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
- leverage, delve, tapestry, elucidate, underscore, unveil, pivotal,
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

- Equation: "as defined in Equation (N)"
- Section: "as described in Section X.Y"
- Figure: "as illustrated in Figure X" / "as shown in Figure X"
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
