# Writing Style Guide for Methodology Sections

> Rules extracted from 9 reference papers and refined with best practices from
> awesome-ai-research-writing, humanizer, and ml-paper-writing.

---

## 1. Prose Structure

### 1.1 Dense Continuous Paragraphs
- **No bullet lists** in the methodology body. All content must be in flowing paragraphs.
- Each paragraph: 100-250 words, one core idea.
- Convert any input notes/bullets into coherent prose before output.

### 1.2 One-Paragraph-One-Topic
- Each paragraph serves exactly one purpose (motivation, formulation, interpretation).
- Do not mix unrelated technical points in a single paragraph.

### 1.3 Logical Connectors
- Use semantic flow rather than mechanical connector stacking.
- Acceptable: "To this end", "Accordingly", "Specifically", "In contrast"
- Avoid overuse of: "Furthermore", "Moreover", "Additionally", "It is worth noting that"
- Never use: "First and foremost", "In light of", "It is imperative to note"

---

## 2. Tense and Voice

### 2.1 Tense Rules
- **Present tense** for method description, architecture, and general claims:
  "The model takes the input features and produces a prediction."
- **Past tense** only for:
  - Citing prior work: "Zhang et al. (2023) proposed a GAN-based approach."
  - Describing completed specific experiments: "The model was trained for 200 epochs."

### 2.2 Voice
- Prefer **active voice** for clarity: "We design a three-stage pipeline" over "A three-stage pipeline is designed."
- **Passive voice** is acceptable for describing standard procedures: "The data is normalized to [0, 1]."
- Avoid first person in Chinese methodology (use passive or impersonal constructions).

---

## 3. Terminology Discipline

### 3.1 Abbreviation Protocol
- Define on first use: "Generative Adversarial Network (GAN)"
- After definition, use only the abbreviation consistently.
- Never re-define the same abbreviation.
- In Chinese text, keep English abbreviations as-is: "生成对抗网络 (GAN)" then "GAN" throughout.

### 3.2 Consistent Naming
- Once a component is named (e.g., "temporal attention module"), use the exact same name everywhere.
- Do not alternate between synonyms (e.g., "temporal attention module" vs "time-wise attention block").

### 3.3 Technical Terms: Keep in English
- In Chinese manuscripts, preserve standard English terms:
  Transformer, GAN, GCN, LSTM, attention, embedding, encoder, decoder, backbone, fine-tuning, pre-training, tokenization, prompt, feature extraction

---

## 4. Equation Conventions

### 4.1 Equation Flow
```
[Motivation sentence] ... is formulated as:

                    Equation (N)

where X denotes ..., Y represents ..., and Z is ...
```

### 4.2 Variable Definition Block
- Always follow an equation with a "where" block.
- Define every symbol that has not been defined earlier.
- Use consistent verbs: "denotes", "represents", "is defined as", "indicates".
- List variables in the order they appear in the equation.

### 4.3 Equation Referencing
- Forward reference: "as defined in Equation (N) below"
- Backward reference: "as given in Equation (M)"
- Cross-section reference: "as described in Section X.Y"

---

## 5. Figure and Table Protocol

### 5.1 Figures
- Reference figures BEFORE they appear in text flow.
- Pattern: "The overall architecture is illustrated in Figure X."
- Never say "The figure shows..." — describe the content directly.
- In Chinese: "如图 X 所示，..." or "图 X 展示了..."

### 5.2 Tables
- Reference tables BEFORE they appear.
- Parameter tables must include: Symbol | Description | Unit (or Value) columns.
- Pattern: "The key parameters are summarized in Table X."

---

## 6. Anti-AI Writing Rules

### 6.1 Words to Avoid (AI-Flavored Vocabulary)
Replace these with simpler alternatives unless technically necessary:

| Avoid | Prefer |
|-------|--------|
| leverage | use, employ, apply |
| delve / delve into | investigate, examine, explore |
| tapestry | context, landscape |
| utilize | use |
| facilitate | enable, allow |
| elucidate | explain, clarify |
| underscore | highlight, show |
| unveil | present, introduce |
| pivotal | important, key, critical |
| intricate | complex |
| nuanced | detailed, subtle |
| foster | support, encourage |
| bolster | strengthen, support |
| endeavor | effort, attempt |
| paramount | important, essential |
| comprehensive | thorough, complete |
| robust | strong, reliable |
| seamless | smooth |
| cutting-edge | recent, advanced, state-of-the-art |
| novel (overuse) | new, proposed (use sparingly) |

### 6.2 Structural Anti-AI Patterns
- **No em-dash (--) abuse**: Use commas, parentheses, or subordinate clauses instead.
- **No rule-of-three stacking**: Avoid "X, Y, and Z" lists that always have exactly 3 items.
- **No significance inflation**: Do not add "significantly", "substantially", "remarkably" unless backed by statistical tests.
- **No promotional language**: Avoid "groundbreaking", "revolutionary", "unprecedented".
- **No filler phrases**: Remove "It is worth noting that", "It should be noted that", "Interestingly".
- **Vary sentence rhythm**: Mix short declarative sentences with longer compound ones. Not every sentence should be the same length.

### 6.3 Possessive Form
- Avoid: "PitGAN's performance", "the model's output"
- Prefer: "the performance of PitGAN", "the output of the model"

---

## 7. Chinese-Specific Style Rules

### 7.1 Punctuation
- Use full-width Chinese punctuation: ，。；：""（）
- Use half-width for numbers, English terms, and math symbols
- Space between Chinese characters and English/numbers: "采用 GAN 模型" not "采用GAN模型"

### 7.2 Formality
- No oral expressions: Replace "我们发现" with "实验结果表明" or "研究表明"
- No subjective tone: Replace "效果很好" with "性能显著提升"
- No archaic bureaucratic style: Avoid "拟", "系", "兹"

### 7.3 Paragraph Transitions
- Rely on semantic flow, not mechanical connectors
- Acceptable: "具体而言", "为此", "在此基础上"
- Avoid stacking: "首先...其次...再次...最后" in every paragraph

---

## 8. Cross-Reference Patterns

### 8.1 Section References
- English: "as described in Section X.Y"
- Chinese: "如第 X.Y 节所述"

### 8.2 Equation References
- English: "as defined in Equation (N)"
- Chinese: "如公式 (N) 所示"

### 8.3 Figure/Table References
- English: "as shown in Figure X" / "as summarized in Table Y"
- Chinese: "如图 X 所示" / "如表 Y 所示"

---

## 9. Output Format Rules (Plain Text for Word)

### 9.1 No Markdown Formatting in Output
- No `**bold**`, `*italic*`, or `# headings` in the generated methodology text.
- No bullet lists (`-`, `*`, `1.`).
- Plain text only, ready to paste into Word.

### 9.2 Section Headers
- Output section headers as plain text with numbering: "3.1 Overall Framework"
- The user will format them in Word.

### 9.3 Equations
- Write equations in plain text notation or describe them verbally.
- Mark equation placeholders: "[Equation (N): description]"
- The user will format equations in Word's equation editor.

