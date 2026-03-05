# Post-Generation Consistency Checklist

> Run this checklist after generating MethodSpec + Chinese + English methodology sections.
> Every item must PASS before delivery. Failed items go to the TODO/VERIFY list.

---

## Phase 1: MethodSpec Integrity

- [ ] **No fabricated values**: Every dataset name, parameter value, hyperparameter, metric, and baseline in MethodSpec comes directly from the user's input (notes, code, config).
- [ ] **No fabricated citations**: Every reference in MethodSpec is either provided by the user or marked as `[CITATION NEEDED]`.
- [ ] **Source traceability**: Every hard fact (numerical value, dataset name, model architecture detail) has a populated `Source:` field. Empty Source fields are treated as FAIL.
- [ ] **Confidence marking**: Every item with `Confidence: NEEDS_VERIFY` has a clear explanation in the TODO/VERIFY list.
- [ ] **Conflict flagging**: If user notes contradict code/config files, the code/config value is used AND the conflict is logged in TODO/VERIFY WITH both Source references.
- [ ] **Completeness**: All required MethodSpec fields have values or explicit `[TBD]` / `[TODO: user to confirm]` markers.

---

## Phase 2: Chinese Methodology (CN)

- [ ] **Structure matches MethodSpec**: Section hierarchy follows MethodSpec outline; no sections added or removed without justification.
- [ ] **Full-width punctuation**: All Chinese punctuation uses full-width characters (，。；：""（）).
- [ ] **Term consistency**: Every technical term matches `term_glossary.yml` CN column.
- [ ] **No oral expressions**: No instances of "我们发现", "效果很好", "很明显" etc.
- [ ] **Equation placeholders**: Every equation is marked as `[公式 (N): description]` for Word insertion.
- [ ] **Figure/table references**: Every figure/table is referenced before its first appearance.
- [ ] **Abbreviation discipline**: Each abbreviation defined on first use, then used consistently.
- [ ] **No Markdown formatting**: Output is plain text — no `**bold**`, `*italic*`, `# heading`, or `- bullet`.

---

## Phase 3: English Methodology (EN)

- [ ] **Structure aligns with CN**: Same section hierarchy, same number of subsections.
- [ ] **Present tense for methods**: Method descriptions use present tense; past tense only for citing prior work.
- [ ] **Term consistency**: Every technical term matches `term_glossary.yml` EN column.
- [ ] **No AI-flavored words**: No instances of leverage, delve, tapestry, utilize, elucidate, underscore, unveil, pivotal, intricate, nuanced, foster, bolster, paramount, comprehensive, robust, seamless, cutting-edge (unless technically required).
- [ ] **No em-dash abuse**: Minimal use of em-dashes; prefer commas, parentheses, or subordinate clauses.
- [ ] **No possessive forms for methods**: Use "the performance of PitGAN" not "PitGAN's performance".
- [ ] **No contractions**: "does not" not "doesn't"; "it is" not "it's".
- [ ] **No bullet lists**: All content in flowing paragraphs.
- [ ] **Equation placeholders**: Every equation marked as `[Equation (N): description]`.
- [ ] **No fabricated references**: All citations either from user input or marked `[CITATION NEEDED]`.
- [ ] **No Markdown formatting**: Plain text output.

---

## Phase 4: CN-EN Cross-Consistency

- [ ] **Aligned section structure**: CN and EN have identical section/subsection numbering.
- [ ] **Aligned equation numbering**: Same equations appear in both versions with same numbers.
- [ ] **Aligned figure/table references**: Same figures and tables referenced in both versions.
- [ ] **Term alignment**: Every CN term maps to its EN counterpart per glossary; no term translated differently across sections.
- [ ] **Symbol alignment**: All mathematical symbols identical in both versions (same notation, same subscripts).
- [ ] **Value alignment**: All numerical values (parameters, metrics, dimensions) identical in both versions.
- [ ] **No content drift**: EN is not a loose paraphrase of CN; both convey the same technical content at the same level of detail.

---

## Phase 5: TODO/VERIFY List Review

- [ ] **All gaps flagged**: Every `[TBD]`, `[TODO]`, `[CITATION NEEDED]`, and `[VERIFY]` marker has been collected into the final TODO/VERIFY list.
- [ ] **Conflict items listed**: All notes-vs-code conflicts are documented with both values and a recommendation.
- [ ] **Actionable items**: Each TODO/VERIFY item specifies what the user needs to provide or confirm.
- [ ] **No silent assumptions**: The skill never silently filled in a missing value — if it had to assume, the assumption is flagged.

---

## Phase 6: Optional Humanizer Pass (if requested)

- [ ] **Technical terms preserved**: All domain-specific terms, model names, and abbreviations unchanged.
- [ ] **Numerical values preserved**: All parameters, metrics, and equation components unchanged.
- [ ] **Equation blocks untouched**: Humanizer did not modify equation placeholders or "where" blocks.
- [ ] **Meaning preserved**: No semantic drift from the pre-humanizer version.
- [ ] **AI patterns reduced**: At least 3 of the 24 humanizer patterns addressed (if present).
- [ ] **Natural rhythm**: Sentence length varies; not all sentences are the same structure.
