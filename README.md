# paper-methodology Skill

OpenCode/Cursor skill for generating bilingual (Chinese + English) Methodology sections for SCI papers in the geotechnical AI domain.

## Domain Scope

- **Geotechnical engineering**: excavation, tunnelling, foundation, underground construction
- **AI/ML methods**: deep learning, GNN, GAN, LLM, physics-informed models, spatiotemporal prediction

## Installation

### Option 1: Use this repository directly

If you're working in this repository, the skill is already available at:
```
.opencode/skills/paper-methodology/
```

OpenCode/Cursor will auto-discover it when you open this project.

### Option 2: Install to global skills directory

Copy the skill to your global OpenCode skills directory:

```bash
# Windows
cp -r .opencode/skills/paper-methodology ~/.config/opencode/skills/

# macOS/Linux
cp -r .opencode/skills/paper-methodology ~/.config/opencode/skills/
```

Or use the OpenSkills CLI (if installed):
```bash
# From this repository root
npx openskills install .opencode/skills/paper-methodology
```

## Usage

### Trigger Keywords

The skill activates when you use phrases like:
- "写方法学" / "write methodology"
- "methods section" / "方法学章节"
- "从脚本生成方法段" / "generate methods from code"
- "bilingual methods"

### Quick Start

Use the one-click command:
```
/methods-bilingual

[Paste your research notes or provide code paths]
```

Or directly prompt:
```
帮我写一篇关于[你的研究主题]的方法学章节。

研究笔记：
- [你的笔记内容]

代码路径：
- model.py
- config.yaml
```

### What You Need to Provide

**Minimum required** (at least one):
- Research notes or outline (can be rough, bullet-point)
- Code repository path or key scripts

**Optional** (improves quality):
- Target journal/conference name
- Architecture diagrams
- Parameter tables
- Draft of other sections for context

### Output

The skill produces 4 sequential outputs:

1. **MethodSpec** — Structured specification for review
2. **Chinese Methodology** — Plain text, Word-ready
3. **English Methodology** — Plain text, Word-ready
4. **TODO/VERIFY List** — Gaps, conflicts, missing citations

## Key Features

### Anti-Hallucination
- Never fabricates datasets, parameters, hyperparameters, or citations
- Code/config values override notes when conflicts occur
- All gaps explicitly flagged as `[TBD]` or `[TODO]`

### Bilingual Consistency
- CN and EN versions generated from single MethodSpec
- Identical structure, equation numbering, figure references
- Aligned terminology via 200+ term glossary

### Word-Ready Output
- Plain text, no Markdown formatting
- Full-width Chinese punctuation
- Equation placeholders for Word equation editor

### Optional Humanizer
- Ask-first de-AI pass for English version
- Preserves all technical terms and numerical values
- Reduces AI writing patterns while maintaining accuracy

## File Structure

```
.opencode/
├── skills/paper-methodology/
│   ├── SKILL.md                    # Main skill definition
│   └── assets/
│       ├── reference_papers/       # 9 source papers (3 own + 6 other)
│       ├── methodology_outline.md  # Flexible section hierarchy
│       ├── style_guide_methodology.md  # Writing rules + de-AI word list
│       ├── term_glossary.yml       # 200+ CN-EN term pairs
│       ├── notation.md             # Symbol conventions
│       └── checklist.md            # Verification checklist
├── commands/
│   └── methods-bilingual.md        # One-click command template
└── regression/
    └── paper-methodology-tests.md  # 5 test cases
```

## Testing

Run the 5 regression tests in `.opencode/regression/paper-methodology-tests.md`:

1. Normal input — excavation surrogate model
2. Missing details — no learning rate specified
3. Notes vs code conflict — batch size mismatch
4. Citation needed — unverifiable reference
5. Optional humanizer — user requests de-AI pass

Each test has clear pass/fail criteria.

## Customization

### Adding New Reference Papers

1. Place full-text `.txt` file in `assets/reference_papers/`
2. Follow naming: `NN-{own|other}-ShortName.txt`
3. Update `assets/reference_papers/README.md`
4. If new terms introduced, add to `assets/term_glossary.yml`

### Extending Term Glossary

Edit `assets/term_glossary.yml` to add new CN-EN term pairs. Categories:
- geotechnical_engineering
- neural_network_fundamentals
- gan, graph_neural_network
- attention_and_transformer, llm
- spatiotemporal, training_and_evaluation
- data_processing, statistical_ml, physics_informed

### Modifying Style Rules

Edit `assets/style_guide_methodology.md` to adjust:
- Prose structure conventions
- Tense and voice rules
- Anti-AI word substitutions
- Chinese-specific formatting

## Limitations

- **Domain-specific**: Only for geotechnical AI papers
- **Methodology only**: Does not generate Introduction, Discussion, or Abstract
- **Plain text output**: Equations must be formatted in Word manually
- **Citation verification**: Cannot auto-fetch BibTeX; user must provide

## Credits

Integrates best practices from:
- [awesome-ai-research-writing](https://github.com/Leey21/awesome-ai-research-writing) — SCI writing prompts
- [humanizer](https://github.com/blader/humanizer) — De-AI writing patterns
- [ml-paper-writing](https://github.com/Orchestra-Research/AI-Research-SKILLs) — Anti-hallucination rules

## License

This skill is for academic research use. Reference papers remain copyright of their respective authors.
