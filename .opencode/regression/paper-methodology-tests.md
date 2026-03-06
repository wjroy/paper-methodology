# Regression Tests for paper-methodology Skill (v3.6)

> 18 test prompts with expected behaviors and pass/fail criteria.
> Tests 1-5: core workflow tests (updated for v3.3 where needed).
> Tests 6-8: style profile, error log, and consistency checker tests.
> Tests 9-11: Source/Confidence traceability and PLAN gate behavior tests.
> Tests 12-13: pattern library selection and inlined prompt-pack capability tests.
> Tests 14-15: section-level refinement scope-lock and MethodSpec sync tests.
> Tests 16-17: logic-enrichment continuity and anti-hallucination guard tests.
> Test 18: calibration-scope split test (rule-refinement full own papers vs runtime lightweight retrieval).
> Use these to verify the skill produces correct output under different conditions.

---

## Test 1: Normal Input — Excavation Surrogate Model

### Prompt
```
帮我写一篇关于基坑变形预测代理模型的方法学章节。

研究笔记：
- 提出一个基于 cGAN 的代理模型（PitGAN），用弹性地基梁模型生成训练数据
- 输入：开挖深度 H、土体弹性模量 E_s、支撑刚度 k
- 输出：围护结构侧向位移曲线 delta_w(z)
- 数据集：3000 组 FEM 模拟数据，按 7:1.5:1.5 划分
- 训练配置：Adam optimizer, lr=0.0002, batch_size=64, 200 epochs
- 评价指标：RMSE, MAE, R^2
- 对比基线：MLP, LSTM, standard GAN
- 框架分三阶段：力学建模 -> 数据生成 -> cGAN 训练与预测

目标期刊：Computers and Geotechnics
```

### Expected Behavior
- [x] Phase A reads style_profile.md, error_log.md, hard_memory.json, soft_memory.json
- [x] Produces complete MethodSpec with all 10 sections filled
- [x] Every hard-fact field in MethodSpec Sections 2-9 has a populated Source and Confidence
- [x] No hard-fact field has a blank Source (Audit Pass 6 would FAIL otherwise)
- [x] PLAN selects a primary methodology pattern before drafting (no single invariant template)
- [x] CN version has opening overview paragraph with method name + figure anchor (numbered steps optional)
- [x] EN version mirrors CN structure exactly
- [x] Section order follows selected pattern overlay and input logic (not forced universal order)
- [x] All numerical values match input (lr=0.0002, batch_size=64, 200 epochs, 3000 samples, 7:1.5:1.5)
- [x] Term glossary terms used consistently (弹性地基梁 = beam on elastic foundation)
- [x] Plain text output, no Markdown formatting
- [x] TODO/VERIFY list is empty or minimal (input is complete)
- [x] Audit summary included with 6-pass results (all PASS expected for complete input)
- [x] Asks about humanizer pass after EN generation

### Pass/Fail
- **PASS**: All expected behaviors satisfied
- **FAIL**: Any fabricated value, missing MethodSpec, structural mismatch between CN/EN, or Markdown in output

---

## Test 2: Missing Details — No Learning Rate Specified

### Prompt
```
Write the methodology section for my shield tunnel settlement prediction model.

Notes:
- Model: GCN + LSTM for spatiotemporal prediction
- Input: 20 monitoring points, each with 5 features
- Output: settlement at next 3 time steps
- Dataset: field monitoring data from Shenzhen Metro Line 14
- Training: used Adam optimizer, 150 epochs
- Metrics: RMSE and MAE
- Baselines: pure LSTM, pure GCN, SVR
```

### Expected Behavior
- [x] MethodSpec marks learning rate as `[TBD: learning rate not specified]` with Source: [TBD], Confidence: NEEDS_VERIFY
- [x] MethodSpec marks batch_size as `[TBD: batch size not specified]` with Source: [TBD], Confidence: NEEDS_VERIFY
- [x] MethodSpec marks train/val/test split as `[TBD: split ratio not specified]` with Source: [TBD], Confidence: NEEDS_VERIFY
- [x] MethodSpec marks graph construction method as `[TBD: adjacency matrix construction not described]` with Source: [TBD], Confidence: NEEDS_VERIFY
- [x] All [TBD] items have matching entries in MethodSpec Section 10 (Conflicts and Gaps)
- [x] TODO/VERIFY list includes at least 4 items for missing information
- [x] Does NOT fabricate a learning rate, batch size, or split ratio
- [x] CN and EN versions use placeholder markers where values are missing

### Pass/Fail
- **PASS**: All missing values flagged as [TBD], no fabricated values
- **FAIL**: Any missing value silently filled in with a default

---

## Test 3: Notes vs Code Conflict — Batch Size Mismatch

### Prompt
```
从我的代码生成方法段。

研究笔记：
- 模型名：MS-STGCN，用于多源数据融合的时空预测
- 训练配置：batch_size=64, lr=0.001, 300 epochs
- 评价指标：RMSE, MAE, MAPE

代码 config.yaml 内容：
batch_size: 32
learning_rate: 0.0005
max_epochs: 300
optimizer: AdamW
scheduler: CosineAnnealingLR
weight_decay: 0.01

注意：以代码为准
```

### Expected Behavior
- [x] MethodSpec uses batch_size=32 with Source: "@config.yaml", Confidence: OK
- [x] MethodSpec uses lr=0.0005 with Source: "@config.yaml", Confidence: OK
- [x] MethodSpec uses AdamW with Source: "@config.yaml", Confidence: OK
- [x] MethodSpec includes scheduler and weight_decay from config with Source: "@config.yaml"
- [x] CONFLICT entries in Section 10: batch_size (notes=64, config=32) and lr (notes=0.001, config=0.0005)
- [x] CN and EN versions both use the code values

### Pass/Fail
- **PASS**: Code values used, conflicts logged, all config details included
- **FAIL**: Notes values used, or conflicts not logged

---

## Test 4: Citation Needed — Unverifiable Reference

### Prompt
```
写方法学，我的模型参考了 Zhang et al. (2024) 提出的物理信息图网络框架。

笔记：
- 在 Zhang et al. 2024 的基础上增加了时间注意力模块
- 使用了 Winkler 地基模型作为物理约束
- 数据来自上海某深基坑项目，共 1500 组监测数据
- 训练用 Adam, lr=0.001, batch=32, 100 epochs
- 指标：RMSE, R^2
```

### Expected Behavior
- [x] Reference to "Zhang et al. (2024)" is preserved as-is (user provided it)
- [x] No additional citations fabricated
- [x] If the specific paper title/venue is not provided, TODO/VERIFY includes: `[CITATION NEEDED: full reference for Zhang et al. (2024) — user to provide title, journal, DOI]`
- [x] Does NOT generate a fake BibTeX entry or guess the paper title
- [x] Winkler foundation model description uses only standard textbook knowledge, not fabricated claims

### Pass/Fail
- **PASS**: Citation preserved, no fabricated references, gap flagged
- **FAIL**: A fake citation is generated, or a BibTeX entry is invented

---

## Test 5: Optional Humanizer — User Requests De-AI Pass

### Prompt
```
Write methodology for my LLM-enhanced risk assessment model.

Notes:
- Two stages: (1) LLM extracts risk factors from construction logs, (2) GNN predicts risk grade
- LLM: fine-tuned GPT-2 with domain-specific corpus
- GNN: 3-layer GAT with 64-dim hidden features
- Risk grades: 4 levels (I-IV)
- Dataset: 500 construction log entries from 3 metro projects
- Training: Adam, lr=0.0001, batch=16, 50 epochs
- Metrics: accuracy, F1-score, precision, recall

After you generate the English version, please apply the humanizer pass.
```

### Expected Behavior
- [x] Recognizes user's pre-authorization of humanizer pass
- [x] Generates all 4 outputs (MethodSpec, CN, EN, TODO/VERIFY)
- [x] Applies humanizer to EN version
- [x] After humanizing, ALL of these are preserved exactly:
  - Model names: GPT-2, GAT, GNN, LLM
  - Parameters: 3-layer, 64-dim, lr=0.0001, batch=16, 50 epochs
  - Dataset: 500 entries, 3 metro projects
  - Risk grades: 4 levels (I-IV)
  - Metrics: accuracy, F1-score, precision, recall
- [x] Humanized version removes at least some AI patterns if present
- [x] Sentence rhythm varies (not all sentences same length)
- [x] No new technical content added during humanization

### Pass/Fail
- **PASS**: Humanizer applied, all technical content preserved, AI patterns reduced
- **FAIL**: Any parameter changed, any model name altered, or humanizer changes technical meaning

---

## Test 6: Style Profile Compliance — Matching User's Writing DNA

### Prompt
```
Write the methodology section for a physics-informed GAN model for predicting
retaining wall deflection under staged excavation.

Notes:
- Model name: PI-WallGAN
- Physics model: Winkler beam model for wall-soil interaction
- Architecture: conditional GAN with physics loss
- Generator: 5-layer MLP with skip connections
- Discriminator: 3-layer MLP
- Physics loss: penalizes violation of equilibrium equations
- Data: 2000 FEM simulations, 80/10/10 split
- Training: Adam, lr=0.0001, batch=32, 300 epochs
- Metrics: RMSE, MAE, R^2
- Baselines: standard cGAN, MLP, LSTM

Please match my usual writing style from my published papers.
```

### Expected Behavior
- [x] Phase A explicitly reads `style_profile.md`
- [x] Opening paragraph names PI-WallGAN and references a framework figure (numbered steps optional)
- [x] PLAN explicitly chooses a pattern (likely physics-mechanism-first or constraint-loss-first) with short rationale
- [x] Paragraphs are 100-250 words each
- [x] Equation introduction uses preferred pattern: "is formulated as:" or "can be expressed as:"
- [x] "Where" blocks use "denotes" and "represents" (not "in which")
- [x] Cross-references use "as defined in Equation (N)" and "as described in Section X.Y"
- [x] EN avoids forced first-person "we" and prefers objective subject style; CN uses "本文/本研究"
- [x] Transition usage is natural and not forced to a fixed connector list
- [x] Technical verbs are from the user's preferred list (propose, employ, design, extract)
- [x] No filler phrases the user avoids ("It is worth noting that", "Interestingly")
- [x] Audit checks style compliance via style_profile.md during Phase C

### Pass/Fail
- **PASS**: Output demonstrably matches the user's style profile patterns
- **FAIL**: Output uses generic academic style that does not match the style profile (e.g., uses "Furthermore/Moreover" stacking, "in which" instead of "where", or opening paragraph does not list numbered steps)

---

## Test 7: Error Log Learning — Avoiding Past Mistakes

### Setup
Before running this test, add the following entry to `error_log.md`:

```
### TERMINOLOGY — Used "foundation pit" instead of "excavation pit"
- Date: 2025-01-15
- Wrong: "The foundation pit deformation is predicted by..."
- Correct: "The excavation pit deformation is predicted by..."
- Context: English methodology, Section 3.1
- Rule: Always use "deep excavation" (not "excavation pit") for 基坑.

### STYLE — Used "It is worth noting that" filler phrase
- Date: 2025-01-16
- Wrong: "It is worth noting that the proposed model outperforms..."
- Correct: "The proposed model outperforms..."
- Context: English methodology, Section 3.5
- Rule: Never use "It is worth noting that" — it is a filler phrase.

### FORMATTING — Markdown bold leaked into plain text output
- Date: 2025-01-17
- Wrong: "The **proposed framework** consists of..."
- Correct: "The proposed framework consists of..."
- Context: English methodology, Section 3.1
- Rule: Output must be plain text. No Markdown formatting (bold, italic, headings, bullets).
```

### Prompt
```
Write methodology for a deep excavation deformation prediction model.

Notes:
- Model: LSTM-based, predicts 基坑 lateral wall displacement
- Input: excavation depth, soil parameters, bracing stiffness
- Output: displacement profile
- Data: 1000 FEM simulations, 70/15/15 split
- Training: Adam, lr=0.001, batch=64, 150 epochs
- Metrics: RMSE, R^2
- Baselines: SVR, MLP
```

### Expected Behavior
- [x] Phase A reads `error_log.md` and identifies 3 logged errors
- [x] EN version uses "excavation pit" (not "foundation pit") for 基坑
- [x] EN version does NOT contain "It is worth noting that"
- [x] EN version does NOT contain Markdown formatting (bold/italic/bullets)
- [x] Audit Pass 5 (Error-log Compliance) reports all PASS

### Pass/Fail
- **PASS**: All 3 logged errors are avoided in the generated output
- **FAIL**: Any of the 3 logged error patterns appear in the output

---

## Test 8: Consistency Checker — Detecting Deliberate Mismatches

### Purpose
Verify the audit system catches CN-EN inconsistencies. This test is run by
manually introducing errors into the draft output and checking whether the
consistency checker identifies them.

### Setup
Generate a normal methodology section (e.g., from Test 1), then manually
introduce these errors before running the audit:

1. Change "batch_size=64" to "batch_size=128" in the EN version only
2. Change "基坑" to "基础坑" in one paragraph of the CN version
3. Remove the "where" block after Equation (2) in the EN version
4. Add a new paragraph about "dropout rate of 0.3" in EN that has no source
5. Change "Section 3.2" reference in EN to "Section 3.3" (wrong cross-reference)

### Expected Behavior
- [x] Audit Pass 2 (Numerical) catches batch_size mismatch between EN and MethodSpec
- [x] Audit Pass 1 (Terminology) catches "基础坑" inconsistency in CN
- [x] Audit Pass 3 (Symbol/Equation) catches missing "where" block in EN
- [x] Audit Pass 6 (Traceability) catches fabricated "dropout rate of 0.3"
- [x] Audit Pass 4 (Structural) catches wrong cross-reference "Section 3.3"

### Pass/Fail
- **PASS**: At least 4 of 5 deliberate errors are caught and reported as FAIL
- **FAIL**: Fewer than 4 errors are caught

---

## Running These Tests

1. Start a new conversation with the paper-methodology skill loaded
2. For tests 1-18: paste each test prompt exactly as shown
3. For test 7: first add the error log entries, then paste the prompt
4. For test 8: generate from test 1, manually introduce errors, then run audit
5. For test 10: verify PLAN gate (Phase B) stops before Phase C until CONFIRM
6. For test 11: verify skip-confirmation mode proceeds directly
7. For test 12: verify pattern selection is explicit and justified
8. For test 13: verify humanizer/polish/logic-check still work after prompt-pack removal
9. For test 14: verify local refinement updates only target subsection
10. For test 15: verify MethodSpec + CN/EN sync under local code-based update
11. For test 16: verify logic-enrichment makes implicit chain explicit
12. For test 17: verify logic-enrichment does not invent unsupported facts
13. For test 18: verify calibration-scope behavior in the explanation output
14. Compare the output against the Expected Behavior checklist
15. Mark each item as pass/fail
16. A test passes only if ALL expected behaviors are satisfied

## Scoring

| Score | Interpretation |
|-------|---------------|
| 18/18 | Skill is production-ready (v3.6 verified) |
| 17/18 | Minor issue — review the failing test and adjust |
| 14-16/18 | Moderate issues — likely need to adjust SKILL.md or an asset file |
| 11-13/18 | Significant issues — structural problem in the workflow |
| <=10/18 | Major revision needed |

## Version History

| Version | Tests | Changes |
|---------|-------|---------|
| v1.0 | 1-5 | Original test suite |
| v2.0 | 1-8 | Added style profile, error log, consistency checker tests |
| v2.1 | 1-11 | Added Source/Confidence traceability and PLAN gate tests |
| v3.1 | 1-11 | Aligned to 3-phase workflow (GATHER/PLAN/WRITE_AUDIT), fixed file paths |
| v3.2 | 1-11 | Strengthened Source/Confidence traceability in Tests 1-3, 9 |
| v3.3 | 1-13 | Added pattern-library selection tests and removed prompt-pack dependency |
| v3.4 | 1-15 | Added section-level refinement tests (scope lock + MethodSpec/CN-EN sync) |
| v3.5 | 1-17 | Added logic-enrichment tests (reasoning continuity + no unsupported facts) |
| v3.6 | 1-18 | Added calibration-scope split test and strengthened local MethodSpec delta expectations |

---

## Test 9: Source Traceability — MethodSpec Must Have Sources

### Prompt
```
Write methodology for my excavation deformation prediction model.

Notes:
- Model: LSTM-based, predicts wall displacement
- Input: excavation depth, soil modulus, bracing stiffness
- Output: displacement profile
- Data: 1000 FEM simulations
- Training: Adam optimizer, 150 epochs
- Metrics: RMSE, R^2
- Baselines: SVR, MLP

Code config.yaml:
learning_rate: 0.001
batch_size: 64
optimizer: Adam
max_epochs: 150
```

### Expected Behavior
- [x] MethodSpec uses template from assets/methodspec_template.md
- [x] Section 2 (Problem Definition): problem statement, inputs, outputs each have Source + Confidence
- [x] Section 5 (Data): data source has Source: "user notes: 1000 FEM simulations", Confidence: OK
- [x] Section 5 (Data): split ratio has Source: [TBD], Confidence: NEEDS_VERIFY (not provided)
- [x] Section 6 (Architecture): LSTM component has Source: "user notes", Confidence: OK
- [x] Section 8 (Training): lr, batch_size, optimizer, epochs all have Source: "@config.yaml#L1-4", Confidence: OK
- [x] Section 9 (Metrics): RMSE, R^2 have Source: "user notes", Confidence: OK
- [x] Section 9 (Baselines): SVR, MLP have Source: "user notes", Confidence: OK
- [x] Section 10 (Conflicts and Gaps): contains [TBD] for split ratio
- [x] No hard-fact field in Sections 2-9 has blank Source
- [x] Audit Pass 6 (Traceability): reports PASS or FLAG (no blank Sources)
- [x] TODO/VERIFY includes action item for the missing split ratio

### Pass/Fail
- **PASS**: All hard facts have populated Source fields with specific references
- **FAIL**: Any hard fact has empty Source field

---

## Test 10: PLAN Gate Enforcement — Must Stop for Confirmation

### Prompt
```
帮我写一篇关于基坑变形预测的方法学章节。

研究笔记：
- 模型：GAN-based surrogate model
- 输入：开挖深度、土体参数
- 输出：位移场
- 数据：2000 组 FEM 数据
- 训练：Adam, lr=0.0002, batch=32, 200 epochs
- 指标：RMSE, MAE
```

### Expected Behavior
- [x] AI completes Phase A (GATHER: parse input, detect conflicts/gaps, load assets)
- [x] AI completes Phase B (PLAN: generates MethodSpec with Source fields)
- [x] AI presents MethodSpec with confirmation prompt including "Reply CONFIRM or OK"
- [x] AI STOPS and waits for user response
- [x] AI does NOT proceed to Phase C (WRITE_AUDIT) automatically

### User Follow-up
After AI stops, reply: `CONFIRM`

Then verify:
- [x] AI proceeds to Phase C (WRITE_AUDIT) only after receiving "CONFIRM"
- [x] AI generates Chinese and English methodology

### Pass/Fail
- **PASS**: AI stops after MethodSpec and waits for explicit confirmation
- **FAIL**: AI proceeds to Phase C automatically without waiting

---

## Test 11: Skip-Confirmation Mode — Exception Handling

### Prompt
```
Write methodology for my shield tunnel settlement prediction model. Skip MethodSpec confirmation and generate directly.

Notes:
- Model: GCN + LSTM
- Input: 20 monitoring points, 5 features each
- Output: settlement at next 3 time steps
- Data: field monitoring from Shenzhen Metro Line 14
- Training: Adam, 150 epochs
- Metrics: RMSE, MAE
- Baselines: pure LSTM, pure GCN, SVR
```

### Expected Behavior
- [x] AI recognizes "skip MethodSpec confirmation" instruction
- [x] AI generates MethodSpec (still required)
- [x] AI does NOT stop for confirmation
- [x] AI proceeds directly to Phase C (WRITE_AUDIT)
- [x] AI generates all 4 outputs (MethodSpec, CN, EN, TODO/VERIFY)

### Pass/Fail
- **PASS**: AI recognizes skip instruction and proceeds without stopping
- **FAIL**: AI ignores instruction and stops for confirmation

---

## Test 12: PLAN Pattern Selection — No Single Invariant Template

### Prompt
```
写方法学：模型是“文本+时序融合”用于轨道沉降分位数预测。

研究笔记：
- 文本数据：施工日志（中文）
- 时序数据：多测点沉降序列
- 文本先做词元化和向量化
- 时序用图结构建模
- 融合后做分位数预测（0.05/0.5/0.95）
- 损失：quantile loss
- 指标：PICP, PINAW, CWC
```

### Expected Behavior
- [x] Phase B first selects a primary pattern (expected: `fusion-pattern` or `data-transformation-first`)
- [x] PLAN gives short rationale and at least one fallback pattern
- [x] Output does not claim an invariant universal section order across all own papers
- [x] Section plan reflects selected overlay (text/time-series encoders -> fusion -> quantile objective)

### Pass/Fail
- **PASS**: Pattern choice is explicit, justified, and reflected in section order
- **FAIL**: Uses a default one-size-fits-all template without pattern selection

---

## Test 13: Prompt-Pack Removal — Inlined Humanizer/Polish/Logic-Check Still Works

### Prompt
```
Write methodology for my multimodal excavation risk model.

Notes:
- Inputs: monitoring time series + construction logs
- Model: graph encoder + text encoder + attention fusion
- Objective: risk level prediction
- Loss: cross-entropy with class weighting
- Metrics: accuracy, macro-F1

After generating EN, apply humanizer and then polish Section 2.2 only.
Also run a logic redline check.
```

### Expected Behavior
- [x] Humanizer runs only because user explicitly requested it
- [x] Humanizer keeps all technical facts unchanged (model, loss, metrics)
- [x] Section-limited polish is applied only to requested subsection
- [x] Logic redline check reports only critical issues (contradictions/term inconsistency/blocking grammar)
- [x] No dependency on `assets/upstream_prompt_pack.md`

### Pass/Fail
- **PASS**: Inlined constraints fully cover humanizer/polish/logic-check behavior
- **FAIL**: Operation fails or still requires external prompt-pack file

---

## Test 14: Section-Level Refinement — Expand 3.2 Only

### Prompt
```
Refine methodology section 3.2 only (expand mode). Do not rewrite other sections.

target_section_or_subsection: 3.2
operation_type: expand

existing_section_text_cn:
3.2 特征提取模块采用双分支结构，分别处理时序监测信号和施工日志文本，随后在共享表示空间中进行融合。

existing_section_text_en:
3.2 The feature extraction module adopts a dual-branch design to process
time-series monitoring signals and construction-log text, followed by fusion in a
shared representation space.

added_notes:
- 时序分支先做 1D convolution 再做 temporal attention
- 文本分支采用 domain vocabulary filtering，去除低信息词
- 融合前对两分支输出进行 layer normalization

added_code_or_config_paths:
- model/fusion_encoder.py
- config/model.yaml
```

### Expected Behavior
- [x] Runs section-level refinement mode (local scope lock)
- [x] MethodSpec updates only fields linked to Section 3.2 (feature extraction/fusion)
- [x] MethodSpec output includes explicit delta tags (`UPDATED`/`UNCHANGED`) for target-linked fields
- [x] CN and EN both update Section 3.2 with aligned technical details
- [x] Sections outside 3.2 are unchanged, except minimal allowed consistency fixes
- [x] No unsourced values are introduced; all new details are traceable to notes/code/config
- [x] Source/Confidence fields are refreshed for every newly added target fact
- [x] Style remains consistent with existing chapter tone

### Pass/Fail
- **PASS**: Only Section 3.2 (and minimal linked fixes) changes; traceability and style consistency preserved
- **FAIL**: Any broad chapter rewrite, or Section 3.2 update contains unsourced details

---

## Test 15: Section-Level Refinement — Code-Driven Correction + CN/EN Sync

### Prompt
```
Please correct subsection 3.4 using the new config. Keep the rest unchanged.

target_section_or_subsection: 3.4
operation_type: correct

existing_section_text_cn:
3.4 损失函数由重建损失和物理约束损失组成，权重分别设为 1.0 与 0.1。

existing_section_text_en:
3.4 The loss function consists of a reconstruction loss and a physics-constraint
loss, with weights set to 1.0 and 0.1, respectively.

added_notes:
- 旧稿中的物理损失权重写错了

added_code_or_config_paths:
- configs/train.yaml  # lambda_phys: 0.25
```

### Expected Behavior
- [x] Uses code/config value (`lambda_phys: 0.25`) over note text
- [x] Updates target MethodSpec loss-related entries and Source/Confidence fields
- [x] MethodSpec delta clearly marks non-target fields as unchanged
- [x] Corrects both CN and EN subsection 3.4 to the same value (0.25)
- [x] Keeps other subsections unchanged unless minimal numbering/term repair is required
- [x] Audit flags PASS for terminology/symbol/numbering/CN-EN alignment in updated scope
- [x] Source/Confidence traceability explicitly covers the corrected weight

### Pass/Fail
- **PASS**: MethodSpec and CN/EN subsection 3.4 are synchronized to code-backed value with no unintended edits elsewhere
- **FAIL**: Value remains inconsistent, source is missing, or unrelated sections are rewritten

---

## Test 16: Logic-Enrichment — Make Implicit Reasoning Chain Explicit

### Prompt
```
Write methodology subsection 3.3 for my multimodal settlement predictor.

Notes:
- Inputs: monitoring time series and construction logs
- Model: temporal encoder + text encoder + fusion layer
- Output: next-step settlement prediction
- Loss: weighted MAE + smoothness constraint

Use compact technical style.
```

### Expected Behavior
- [x] Draft does not stop at module listing; it explains each module's functional role
- [x] At least one local input -> operation -> output chain is explicit
- [x] Includes handoff logic from encoded features to fusion, and from fusion to prediction head
- [x] Loss/constraint is described with pipeline purpose (what behavior it enforces)
- [x] Formula/module mentions are connected to role and not isolated
- [x] Tone remains compact and technical (not tutorial-like)
- [x] Enrichment style remains own-paper aligned (no generic motivational filler)

### Pass/Fail
- **PASS**: Reasoning continuity is visibly improved (purpose, transformation, and handoff are explicit) while style remains concise
- **FAIL**: Output still reads as disconnected module list or abrupt step jumps

---

## Test 17: Logic-Enrichment Safety — No Unsupported Fact Injection

### Prompt
```
Write methodology for a risk prediction model using:
- graph encoder
- temporal decoder
- weighted loss

Known facts only:
- metric: RMSE
- optimizer: Adam

Do not ask for extra info; proceed with placeholders if needed.
```

### Expected Behavior
- [x] Logic-enrichment pass improves continuity using only provided facts
- [x] No fabricated hyperparameters (e.g., lr, batch size, hidden size) are introduced
- [x] No fabricated modules, citations, datasets, or results are introduced
- [x] Missing values remain [TBD]/[VERIFY] and appear in TODO/VERIFY
- [x] MethodSpec Source/Confidence traceability remains intact for enriched prose
- [x] CN and EN remain aligned after enrichment

### Pass/Fail
- **PASS**: Logic becomes clearer without adding unsupported facts; traceability remains valid
- **FAIL**: Any new unsupported value/module/citation/result appears in enriched text

---

## Test 18: Calibration Scope Split — Full Own-Paper Rules vs Lightweight Runtime

### Prompt
```
Before generating, explain your retrieval strategy for style/pattern calibration.

Then write only subsection 3.2 (rewrite mode) for a multimodal excavation model.

target_section_or_subsection: 3.2
operation_type: rewrite
existing_section_text_en:
3.2 The module extracts text and time-series features and fuses them.
added_notes:
- text branch uses domain vocabulary filtering
- time-series branch uses temporal convolution
- fusion uses attention weighting

Keep runtime lightweight.
```

### Expected Behavior
- [x] Explanation explicitly distinguishes:
  - rule-refinement phase uses all own papers 01-05
  - runtime generation uses only top relevant own papers (2-3 by default)
- [x] Runs section-level refinement instead of full-chapter generation
- [x] Updates only target-linked MethodSpec entries and returns MethodSpec delta
- [x] Applies logic-enrichment in rewritten subsection without unsupported additions
- [x] Keeps non-target sections untouched except minimal linked consistency edits

### Pass/Fail
- **PASS**: Phase split is explicit and local rewrite remains scoped, traceable, and lightweight
- **FAIL**: Claims runtime must read all own papers every time, or performs broad chapter rewrite

---

## Version History Update

See "Version History" section above.
