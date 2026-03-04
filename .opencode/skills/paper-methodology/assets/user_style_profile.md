# User Style Profile — Writing DNA

> Auto-generated from analysis of the user's 3 published papers:
> - 01-own-PitGAN (excavation surrogate model with cGAN)
> - 02-own-PI-ETGCN (physics-informed spatiotemporal GCN)
> - 03-own-THGAN (tunnel hybrid GAN)
>
> This file is read by the AI before every text generation. Patterns marked HIGH
> are mandatory to follow; MEDIUM patterns are strongly preferred; LOW patterns
> are optional guidelines.
>
> Last updated: Initial extraction from 3 papers.
> To update: Run `style_extractor.md` on new papers and merge results.

---

## 1. Structural Patterns

### 1.1 Opening Paragraph

**Pattern**: Every methodology section opens with exactly 1 paragraph that:
- Names the proposed method/framework
- Lists 3-4 numbered high-level steps or components
- References the overall framework figure
- Word count: ~100-150 words

**Confidence**: HIGH (all 3 papers)

**EN example** [Paper 01 — PitGAN]:
"The proposed PitGAN framework consists of three main stages: (1) physics-based
mechanical modeling of the excavation system, (2) synthetic data generation through
parametric analysis, and (3) conditional GAN training and displacement prediction.
The overall architecture is illustrated in Figure 2."

**CN pattern**:
"本研究提出的 [METHOD] 框架主要包含以下几个步骤：（1）...；（2）...；（3）...。
图 X 展示了该方法的总体框架。"

### 1.2 Section Ordering

**Pattern**: Physics-first ordering — the analytical/mechanical model always
precedes the neural network architecture.

**Confidence**: HIGH (all 3 papers)

**Typical hierarchy**:
```
X. Methodology
   X.1 Overall Framework (overview paragraph + figure ref)
   X.2 Physical/Mechanical Modeling
   X.3 Data Generation/Processing
   X.4 Model Architecture
       X.4.1 Component A
       X.4.2 Component B
       X.4.3 Component C
   X.5 Loss Function and Training
   X.6 Evaluation Metrics (sometimes moved to Experiments)
```

### 1.3 Subsection Structure

**Pattern**: Each subsection typically has 2-5 paragraphs. Each paragraph focuses
on one technical component or derivation step.

**Confidence**: HIGH

**Sub-pattern**: Subsections open with a 1-2 sentence motivation before diving into
formulation. They do NOT open with the equation directly.

---

## 2. Equation Integration Style

### 2.1 Introduction Patterns

**Preferred patterns** (ranked by frequency):
1. "X is formulated as:" — most common
2. "X can be expressed as:" — for derived quantities
3. "The [COMPONENT] is defined as:" — for definitions
4. "Mathematically, X is computed as:" — occasional

**Confidence**: HIGH

### 2.2 "Where" Block Style

**Pattern**:
- Uses "where" (not "in which")
- Preferred verbs: "denotes" (most common), "represents", "is defined as"
- Variables listed in the order they appear in the equation
- Typically NO closing interpretation sentence after the "where" block —
  interpretation comes in the next paragraph

**Confidence**: HIGH

**EN example**: "where X denotes the input feature matrix, W represents the
learnable weight parameters, and sigma() is the activation function."

**CN example**: "其中，X 表示输入特征矩阵，W 代表可学习的权重参数，sigma() 为激活函数。"

### 2.3 Cross-Referencing

**Preferred patterns**:
- Equations: "as defined in Equation (N)" — not "Eq. (N)"
- Sections: "as described in Section X.Y"
- Figures: "as illustrated in Figure X" or "as shown in Figure X"
- Tables: "as summarized in Table X"
- CN: "如公式 (N) 所示", "如第 X.Y 节所述", "如图 X 所示"

**Confidence**: HIGH (consistent across all 3 papers)

---

## 3. Voice and Tense Patterns

### 3.1 Active vs. Passive Ratio

**Pattern**: Approximately 60% active, 40% passive.
- Active for design decisions: "We design a three-stage pipeline..."
- Active for method descriptions: "The model takes the input features and produces..."
- Passive for standard procedures: "The data is normalized to [0, 1]."
- Passive for data descriptions: "The dataset is split into training, validation, and test sets."

**Confidence**: HIGH

### 3.2 First-Person Usage

**EN**: Moderate use of "we" — appears 5-10 times per methodology section.
- "We design...", "We propose...", "We employ..."
- Not overused; alternates with "The proposed method..." and passive voice.

**CN**: Uses "本文" and "本研究" rather than "我们".
- "本文提出的方法...", "本研究采用...", "为了解决...问题，本文设计了..."
- Impersonal constructions preferred in Chinese.

**Confidence**: HIGH

### 3.3 Tense

**Pattern**:
- Present tense for all method descriptions (no exceptions found)
- Past tense ONLY for citing published prior work
- "The model is trained for 200 epochs" — present tense even for training
  (describing the method, not a completed experiment)

**Confidence**: HIGH

---

## 4. Vocabulary Preferences

### 4.1 Transition Phrases (Top 10)

| Rank | EN Phrase | CN Equivalent | Frequency |
|------|-----------|---------------|-----------|
| 1 | Specifically | 具体而言 | Very high |
| 2 | To this end | 为此 | High |
| 3 | In particular | 特别地 | High |
| 4 | To be more specific | 更具体地 | Medium |
| 5 | Accordingly | 因此 | Medium |
| 6 | In this study | 本研究中 | Medium |
| 7 | As illustrated in Figure X | 如图 X 所示 | High |
| 8 | In contrast | 相比之下 | Medium |
| 9 | Subsequently | 随后 | Medium |
| 10 | On this basis | 在此基础上 | Medium |

**Phrases the user AVOIDS**:
- "It is worth noting that" — never used
- "Interestingly" — never used
- "Furthermore" / "Moreover" stacking — rare
- "First and foremost" — never used

**Confidence**: HIGH (extracted from all 3 papers)

### 4.2 Technical Verbs

| Context | Preferred | Sometimes Used | Avoided |
|---------|-----------|----------------|---------|
| Introducing method | propose, present | introduce | put forward |
| Using a technique | employ, adopt | use, apply | utilize, leverage |
| Achieving results | achieve | obtain | attain, garner |
| Designing components | design | develop | craft, architect |
| Processing data | process | handle | manipulate |
| Extracting features | extract | capture | harvest, glean |

**Confidence**: HIGH

### 4.3 Recurring Methodology Phrases

These phrases appear in 2+ of the user's papers:
- "The overall framework is illustrated in Figure X."
- "The proposed [METHOD] framework consists of [N] main components:"
- "To address the challenge of [PROBLEM], this study proposes [METHOD]."
- "The mathematical formulation is detailed as follows."
- "as described in Section X.Y"
- "The key parameters are summarized in Table X."
- "where [VAR] denotes [DEF], [VAR] represents [DEF], and [VAR] is [DEF]."

**Confidence**: HIGH

### 4.4 AI-Flagged Words Natural Usage

Words from the anti-AI list that the user naturally uses (DO NOT remove these):
- "comprehensive" — used sparingly, in valid technical contexts
- "robust" — used to describe model performance with statistical backing

Words the user never uses (safe to flag):
- leverage, delve, tapestry, elucidate, underscore, unveil, pivotal, intricate,
  nuanced, foster, bolster, endeavor, paramount, seamless, cutting-edge

**Confidence**: HIGH

---

## 5. Paragraph Architecture

### 5.1 Opening Sentences

**Pattern**: Topic sentence stating the paragraph's purpose.
- "The [COMPONENT] module is designed to [PURPOSE]."
- "To capture the [PROPERTY], we employ [TECHNIQUE]."
- "The training procedure follows a [DESCRIPTION] strategy."

**Confidence**: HIGH

### 5.2 Closing Sentences

**Pattern**: Mixed — no single dominant closing pattern.
- Sometimes: transition to next topic ("The extracted features are then fed to...")
- Sometimes: summary of the component just described
- Sometimes: equation reference as the final element
- Rarely: standalone interpretation sentence

**Confidence**: MEDIUM

### 5.3 Internal Flow

**Dominant pattern**: Motivation → Formulation → Variable Definition
1. Open with WHY this component/equation is needed (1-2 sentences)
2. Present the formulation or equation
3. Define variables in "where" block
4. Optional: brief interpretation or connection to next component

**Confidence**: HIGH

---

## 6. Chinese-Specific Patterns

### 6.1 Punctuation
- Full-width Chinese punctuation throughout: ，。；：""（）
- Half-width for numbers, English terms, math symbols

### 6.2 Spacing
- Space between Chinese characters and English terms: "采用 GAN 模型"
- Space between Chinese characters and numbers: "共 3000 组数据"

### 6.3 Register
- Formal academic: "本文提出", "本研究采用", "实验结果表明"
- Never uses oral expressions: no "我们发现", no "效果很好"

### 6.4 English Term Retention
- Keep in English: all model names (GAN, GCN, LSTM, Transformer, etc.),
  standard abbreviations (RMSE, MAE, Adam), activation function names (ReLU, sigmoid)
- Translate to Chinese: general concepts (deep learning → 深度学习,
  loss function → 损失函数, training set → 训练集)

**Confidence**: HIGH (all patterns consistent across papers)

---

## 7. Usage Instructions for the AI

Before generating any methodology text, read this entire file and:

1. **Match structural patterns**: Use the same opening paragraph format, section
   ordering, and subsection depth as described in Section 1.
2. **Match equation style**: Introduce equations using the patterns in Section 2.
   Use "where" (not "in which"), use "denotes/represents".
3. **Match voice**: Maintain ~60/40 active/passive ratio. Use "we" moderately
   in English, use "本文/本研究" in Chinese.
4. **Match vocabulary**: Use the preferred transition phrases and technical verbs
   from Section 4. Avoid the phrases marked as avoided.
5. **Match paragraph flow**: Follow the Motivation → Formulation → Definition
   pattern from Section 5.
6. **Match Chinese conventions**: Follow spacing, punctuation, and register
   rules from Section 6.
