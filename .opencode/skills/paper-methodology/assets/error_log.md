# Error Log — Persistent Correction Memory

> This file records user corrections from past sessions. The AI MUST read this
> file before every text generation and avoid repeating any logged mistake.
>
> Format: Each entry is a correction the user made. The AI should treat these
> as "negative constraints" — things that must NOT appear in future output.
>
> Maintenance: The AI appends new entries when the user corrects its output.
> Entries are never deleted (they accumulate as learning).

---

## How to Use This File

### Before Generation (AI reads)
1. Read all entries below.
2. For each entry, internalize the correction as a rule.
3. During drafting, actively check against these rules.
4. If uncertain whether a pattern matches a logged error, err on the side of
   following the correction.

### After User Correction (AI writes)
When the user corrects your output, append a new entry using this format:

```
### [CATEGORY] — Brief Description
- Date: YYYY-MM-DD
- Wrong: [what the AI produced]
- Correct: [what the user wanted]
- Context: [which section/paper this occurred in]
- Rule: [the general rule to prevent recurrence]
```

### Categories
- TERMINOLOGY: wrong term choice or inconsistent term usage
- FORMATTING: punctuation, spacing, Markdown leaks, structure issues
- STYLE: tone, voice, register, or vocabulary problems
- FACTUAL: incorrect technical claims or fabricated values
- STRUCTURAL: wrong section ordering, missing sections, alignment issues
- TRANSLATION: CN-EN mismatch, mistranslation, or inconsistent rendering

---

## Error Entries

> No errors logged yet. This section will grow as the user provides corrections.
> Each correction becomes a permanent rule for future generations.

<!-- 
Example entry (for reference — delete this comment block after first real entry):

### TERMINOLOGY — Used "foundation pit" instead of "excavation pit"
- Date: 2025-01-15
- Wrong: "The foundation pit deformation is predicted by..."
- Correct: "The excavation pit deformation is predicted by..."
- Context: English methodology, Section 3.1
- Rule: Always use "excavation pit" (not "foundation pit") for 基坑. See term_glossary.yml.

### STYLE — Used "It is worth noting that" filler phrase
- Date: 2025-01-15
- Wrong: "It is worth noting that the model achieves higher accuracy..."
- Correct: "The model achieves higher accuracy..."
- Context: English methodology, Section 3.4
- Rule: Never use "It is worth noting that" — it is a filler phrase. State the point directly.

### FORMATTING — Markdown bold leaked into plain text output
- Date: 2025-01-16
- Wrong: "The **proposed framework** consists of..."
- Correct: "The proposed framework consists of..."
- Context: English methodology, Section 3.1
- Rule: Output must be plain text. No Markdown formatting (bold, italic, headings, bullets).
-->
