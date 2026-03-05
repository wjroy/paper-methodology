# Consistency Checker — Dedicated Audit Prompt

> This file defines a rigorous consistency audit to run after drafting both the
> Chinese and English methodology sections. It replaces the lightweight Phase 5
> checklist with a structured multi-pass audit that produces an actionable report.
>
> When to run: After DRAFT step completes (both CN and EN versions generated).
> The AI runs this audit internally, fixes what it can, and reports remaining
> issues in the TODO/VERIFY list.

---

## Audit Procedure

Run each audit pass in sequence. Each pass produces PASS / FLAG / FAIL results.
FAIL items must be fixed before delivery. FLAG items go to TODO/VERIFY.

---

### Pass 1: Terminology Consistency Audit

**Scope**: Both CN and EN versions + MethodSpec

**Procedure**:
1. Extract every technical term from the CN version.
2. For each term, look up in `term_glossary.yml`:
   - If found: verify the EN version uses the matching EN term.
   - If not found: flag as potential glossary gap.
3. Check within each version:
   - Does the same concept use the same term throughout? (no synonym cycling)
   - Is every abbreviation defined on first use?
   - After first use, is only the abbreviation used (not the full form again)?
4. Check against `memory/hard_memory.json` `critical_terms`:
   - Every critical term must use the exact mapping from hard_memory.

**Output format**:
```
TERMINOLOGY AUDIT
  [PASS] 基坑 = excavation pit — consistent throughout
  [PASS] GAN — defined on first use in both versions
  [FAIL] CN uses "基础坑" in Section 3.2 but "基坑" elsewhere — fix to "基坑"
  [FLAG] Term "latent space" not in glossary — add to glossary or verify
```

---

### Pass 2: Numerical Value Audit

**Scope**: MethodSpec + CN version + EN version

**Procedure**:
1. Extract every number from the MethodSpec (parameters, dimensions, counts, ratios).
2. For each number, verify it appears identically in:
   - The CN version (same value, same context)
   - The EN version (same value, same context)
3. Check that no numbers exist in CN or EN that are NOT in the MethodSpec.
   (This catches fabricated values that bypassed the MethodSpec.)
4. Cross-check against `memory/hard_memory.json` `standard_units`:
   - Every number should have the correct unit.

**Output format**:
```
NUMERICAL VALUE AUDIT
  [PASS] batch_size=32 — MethodSpec, CN, EN all match
  [PASS] lr=0.0002 — MethodSpec, CN, EN all match
  [FAIL] MethodSpec says 3000 samples, EN says 3500 — fix EN to 3000
  [FLAG] CN mentions "5 层" but MethodSpec does not specify layer count — add to MethodSpec or mark [TBD]
```

---

### Pass 3: Symbol and Equation Audit

**Scope**: Both CN and EN versions

**Procedure**:
1. List every equation placeholder in the CN version: [公式 (1)], [公式 (2)], ...
2. List every equation placeholder in the EN version: [Equation (1)], [Equation (2)], ...
3. Verify 1:1 correspondence: same equations, same numbering, same order.
4. For each equation, verify:
   - Every symbol in the equation has a definition in the "where" block.
   - Every symbol in the "where" block appears in the equation.
   - Symbol names match `notation.md` conventions.
   - The "where" block in CN uses the same symbols as the EN "where" block.
5. Check cross-references:
   - Every "Equation (N)" reference points to an existing equation.
   - No equation is defined but never referenced.

**Output format**:
```
SYMBOL & EQUATION AUDIT
  [PASS] Equation (1) — present in both CN and EN, symbols match
  [FAIL] Equation (3) CN has symbol "beta" but EN has "B" — standardize to "beta"
  [FLAG] Symbol "gamma" defined in where block but does not appear in equation — remove or fix equation
  [PASS] All equation cross-references are valid
```

---

### Pass 4: Structural Alignment Audit

**Scope**: CN version vs EN version

**Procedure**:
1. Extract section hierarchy from CN: list all section/subsection numbers and titles.
2. Extract section hierarchy from EN: list all section/subsection numbers and titles.
3. Verify:
   - Same number of sections and subsections.
   - Same numbering scheme.
   - Titles are semantic equivalents (not just translations — check they refer to the same content).
4. For each section pair (CN-EN):
   - Same number of paragraphs (allow +-1 for language-natural differences).
   - Same number of equation placeholders.
   - Same figure/table references.
5. Check that no section in one version has content with no counterpart in the other.

**Output format**:
```
STRUCTURAL ALIGNMENT AUDIT
  [PASS] Section 3.1 — CN "总体框架" / EN "Overall Framework" — aligned
  [PASS] Section 3.2 — CN 4 paragraphs / EN 4 paragraphs — matched
  [FAIL] Section 3.4 — CN has 3 equations, EN has 2 — missing Equation (7) in EN
  [FLAG] CN Section 3.3 has 5 paragraphs, EN has 3 — significant length difference
```

---

### Pass 5: Style Profile Compliance Audit

**Scope**: Both CN and EN versions, checked against `user_style_profile.md`

**Procedure**:
1. **Opening paragraph**: Does it match the pattern from style profile Section 1.1?
   - Lists numbered steps? References framework figure? ~100-150 words?
2. **Section ordering**: Does it follow the physics-first pattern?
3. **Equation style**: Are equations introduced with preferred patterns from style profile Section 2?
4. **Voice**: Approximately 60/40 active/passive ratio in EN?
5. **Vocabulary**: Are preferred transition phrases used? Are avoided phrases absent?
6. **Paragraph length**: Are paragraphs within 100-250 words?
7. **CN conventions**: Full-width punctuation? Spaces between CN and EN terms?

**Output format**:
```
STYLE COMPLIANCE AUDIT
  [PASS] Opening paragraph — matches pattern (3 numbered steps, figure ref, 135 words)
  [PASS] Section ordering — physics model before architecture
  [FLAG] Paragraph in Section 3.4 is 280 words — exceeds 250-word guideline, consider splitting
  [FAIL] Uses "It is worth noting that" in Section 3.3 — remove (user never uses this phrase)
  [PASS] CN punctuation — all full-width
```

---

### Pass 6: Error Log Compliance Audit

**Scope**: Both CN and EN versions, checked against `error_log.md`

**Procedure**:
1. Read all entries in `error_log.md`.
2. For each entry, check whether the generated text contains the same mistake.
3. If a logged error pattern is found in the new output: FAIL (must fix before delivery).

**Output format**:
```
ERROR LOG AUDIT
  [PASS] No logged errors found in generated text
  — or —
  [FAIL] Error log entry "TERMINOLOGY — Used 'foundation pit'" matched in EN Section 3.1 — fix to "excavation pit"
```

---

### Pass 7a: Source Traceability Audit

**Scope**: MethodSpec only

**Procedure**:
1. For every hard fact in the MethodSpec (numerical values, dataset names, architecture details, hyperparameters):
   - Check that the `Source:` field is populated (not empty).
   - Verify the source reference is specific (e.g., `@config.yaml#L10` not just "config file").
2. For every item with `Confidence: NEEDS_VERIFY`:
   - Check that there is a corresponding entry in Section 10: CONFLICTS & GAPS.
3. For every conflict between notes and code:
   - Verify both sources are cited: `Source: user notes say X; code @file.py#L5 says Y; using Y (code wins)`.

**Output format**:
```
SOURCE TRACEABILITY AUDIT
  [PASS] batch_size=32 — Source: @config.yaml#L8, Confidence: OK
  [PASS] learning_rate=0.0002 — Source: @train.py#L45, Confidence: OK
  [FAIL] "3000 samples" — Source field is empty — add source or mark [TBD]
  [FLAG] "excavation depth range 5-15m" — Confidence: NEEDS_VERIFY but no explanation in Section 10 — add to CONFLICTS & GAPS
```

---

### Pass 7b: Anti-Hallucination Audit

**Scope**: MethodSpec + both versions

**Procedure**:
1. For every dataset name, parameter value, hyperparameter, metric, and baseline in the text: trace it back to the MethodSpec Source field.
2. If a value in CN/EN text cannot be traced to a MethodSpec Source: FAIL — mark as [TBD] and add to TODO/VERIFY.
3. For every citation: verify it was provided by the user, not generated.
4. Check that no equation, model name, or technique was introduced that the user did not mention.

**Output format**:
```
ANTI-HALLUCINATION AUDIT
  [PASS] All parameter values traced to MethodSpec with valid Source
  [FAIL] "dropout rate of 0.3" appears in EN Section 3.4 but MethodSpec has no Source for this — remove or mark [TBD]
  [FLAG] Citation "Zhang et al. (2024)" — user provided name but not full reference — add [CITATION NEEDED]
```

---

## Audit Summary Template

After all 7 passes, compile:

```
CONSISTENCY AUDIT SUMMARY
=========================

Pass 1 (Terminology):   X PASS / Y FLAG / Z FAIL
Pass 2 (Numerical):     X PASS / Y FLAG / Z FAIL
Pass 3 (Symbol/Eq):     X PASS / Y FLAG / Z FAIL
Pass 4 (Structure):     X PASS / Y FLAG / Z FAIL
Pass 5 (Style):         X PASS / Y FLAG / Z FAIL
Pass 6 (Error Log):     X PASS / Y FLAG / Z FAIL
Pass 7 (Hallucination): X PASS / Y FLAG / Z FAIL

TOTAL: [N] items checked, [F] FAIL, [G] FLAG, [P] PASS

Action Required:
  - [F] FAIL items have been auto-fixed in the text above.
  - [G] FLAG items are listed in the TODO/VERIFY output.
```

---

## Post-Audit Actions

1. **FAIL items**: Fix in-place. Update both CN and EN versions. Re-run the
   specific audit pass to confirm the fix.
2. **FLAG items**: Add to the TODO/VERIFY list with clear action descriptions.
3. **PASS items**: No action needed.
4. If any FAIL items were found and fixed, note them in the final output:
   "Consistency audit found and auto-corrected N issues. See TODO/VERIFY for
   M items requiring user attention."
