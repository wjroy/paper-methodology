# Style Extractor — Writing DNA Analysis Prompt

> This file is a structured prompt for extracting the user's personal writing style
> ("Style DNA") from their published papers. Run this analysis on the user's own
> papers in `reference_papers/01-own-*.txt` through `03-own-*.txt` to populate
> `user_style_profile.md`.
>
> When to run: (1) Initial skill setup, (2) When the user publishes a new paper
> and wants to update their style profile.

---

## Instructions for the AI

Read all files matching `reference_papers/0*-own-*.txt` (the user's own published
papers). For each paper, extract the Methodology/Methods section only. Then analyze
across all papers to identify consistent patterns. Populate each section of
`user_style_profile.md` with your findings.

### Step 1: Structural Patterns

For each paper's methodology section, record:

1. **Opening paragraph**: Copy the first paragraph verbatim. Identify:
   - Does it list numbered steps? How many (3, 4, 5)?
   - Does it name all major components/modules?
   - Does it reference a framework figure?
   - Approximate word count.

2. **Section hierarchy**: Record the exact section/subsection numbering and titles.
   Identify the ordering pattern:
   - Physics model before or after neural architecture?
   - Data section before or after architecture?
   - Where does loss function appear?
   - Where do evaluation metrics appear?

3. **Subsection structure**: For each subsection, note:
   - Number of paragraphs
   - Average paragraph word count
   - Whether it opens with motivation or jumps to formulation
   - Whether it closes with a summary/transition sentence

### Step 2: Equation Integration Style

For each equation in the methodology sections:

1. **Introduction pattern**: What sentence pattern precedes the equation?
   - "X is formulated as:" / "X can be computed as:" / "X is defined as:"
   - Record the 3-5 most common patterns.

2. **"Where" block style**:
   - Does the author use "where" or "in which"?
   - What verbs: "denotes", "represents", "is defined as", "indicates"?
   - Are variables listed in equation order or grouped by type?
   - Is there a closing interpretation sentence after the "where" block?

3. **Cross-referencing**: Record exact patterns used:
   - "as defined in Equation (N)" / "as shown in Eq. (N)" / other?
   - "as described in Section X.Y" / "as discussed in Section X.Y" / other?
   - "as illustrated in Figure X" / "as shown in Fig. X" / other?

### Step 3: Voice and Tense Patterns

Analyze across all methodology sections:

1. **Active vs. passive ratio**: Count instances of:
   - Active: "We design...", "We propose...", "The model takes..."
   - Passive: "The features are extracted...", "The loss is defined..."
   - Estimate the ratio.

2. **First-person usage**: How frequently does "we" appear?
   - "We design", "We propose", "We employ" — or avoided entirely?
   - In Chinese: is "本文" / "本研究" used, or impersonal constructions?

3. **Tense consistency**:
   - Present tense for methods (confirm or note exceptions)
   - Past tense for citations (confirm or note exceptions)
   - Any mixed-tense patterns?

### Step 4: Vocabulary Preferences

Extract the user's preferred words and phrases:

1. **Transition phrases** (record top 10 most frequently used):
   - e.g., "To this end", "Specifically", "In particular", "To be more specific"
   - Note any phrases the user never uses.

2. **Technical verbs** (record preferences):
   - "employ" vs "use" vs "apply" vs "adopt"
   - "propose" vs "present" vs "introduce"
   - "achieve" vs "obtain" vs "attain"

3. **Methodology-specific phrases** (verbatim recurring phrases):
   - e.g., "The overall framework is illustrated in Figure X."
   - e.g., "The proposed method consists of N main components:"
   - Record any phrase that appears in 2+ papers.

4. **Words the user avoids**:
   - Check against the anti-AI word list. Does the user naturally avoid them?
   - Note any AI-flagged words the user does use naturally.

### Step 5: Paragraph Architecture

Analyze paragraph-level patterns:

1. **Opening sentences**: What pattern does the first sentence of each paragraph follow?
   - Topic sentence stating the paragraph's purpose?
   - Motivation sentence explaining why?
   - Continuation from previous paragraph?

2. **Closing sentences**: How do paragraphs end?
   - Summary of what was just described?
   - Transition to next topic?
   - Equation reference?
   - Simply ends after the last technical point?

3. **Internal structure**: Within a paragraph, what is the flow?
   - Motivation → formulation → interpretation?
   - Claim → evidence → implication?
   - General → specific → example?

### Step 6: Chinese-Specific Patterns

For the Chinese versions (if available in the user's papers):

1. **Punctuation patterns**: Full-width usage consistency.
2. **Spacing**: Space between Chinese and English terms?
3. **Register**: Formal academic ("本文提出") vs. slightly less formal ("我们提出")?
4. **English term retention**: Which terms are kept in English vs. translated?

---

## Output Format

Populate `user_style_profile.md` with your findings using its template structure.
For each field, provide:
- The extracted pattern
- 1-2 verbatim examples from the user's papers (with paper ID, e.g., "[Paper 01]")
- Confidence level: HIGH (consistent across all papers) / MEDIUM (2 of 3 papers) / LOW (1 paper only)
