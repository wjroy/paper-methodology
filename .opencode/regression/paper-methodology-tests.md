# Regression Tests for paper-methodology Skill (v3.1)

> 11 test prompts with expected behaviors and pass/fail criteria.
> Tests 1-5: original tests (unchanged, still valid).
> Tests 6-8: style profile, error log, and consistency checker tests.
> Tests 9-11: Source/Confidence traceability and PLAN gate behavior tests.
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
- [x] CN version has opening overview paragraph with 3 numbered steps
- [x] EN version mirrors CN structure exactly
- [x] Physics model (elastic foundation beam) precedes neural network architecture
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
- [x] Opening paragraph matches the user's pattern: names PI-WallGAN, lists numbered steps, references a figure
- [x] Physics-first ordering: Winkler beam model section precedes GAN architecture
- [x] Paragraphs are 100-250 words each
- [x] Equation introduction uses preferred pattern: "is formulated as:" or "can be expressed as:"
- [x] "Where" blocks use "denotes" and "represents" (not "in which")
- [x] Cross-references use "as defined in Equation (N)" and "as described in Section X.Y"
- [x] EN uses "we" moderately (5-10 times); CN uses "本文/本研究"
- [x] Transition phrases are from the user's preferred list (Specifically, To this end, In particular)
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
- Rule: Always use "excavation pit" (not "foundation pit") for 基坑.

### STYLE — Used "It is worth noting that" filler phrase
- Date: 2025-01-16
- Wrong: "It is worth noting that the proposed model outperforms..."
- Correct: "The proposed model outperforms..."
- Context: English methodology, Section 3.5
- Rule: Never use "It is worth noting that" — it is a filler phrase.

### FORMATTING — Used "Eq." abbreviation instead of "Equation"
- Date: 2025-01-17
- Wrong: "as defined in Eq. (3)"
- Correct: "as defined in Equation (3)"
- Context: English methodology, throughout
- Rule: Always write "Equation" in full, never abbreviate to "Eq."
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
- [x] EN version uses "Equation (N)" not "Eq. (N)" for equation references
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
2. For tests 1-11: paste each test prompt exactly as shown
3. For test 7: first add the error log entries, then paste the prompt
4. For test 8: generate from test 1, manually introduce errors, then run audit
5. For test 10: verify PLAN gate (Phase B) stops before Phase C until CONFIRM
6. For test 11: verify skip-confirmation mode proceeds directly
7. Compare the output against the Expected Behavior checklist
8. Mark each item as pass/fail
9. A test passes only if ALL expected behaviors are satisfied

## Scoring

| Score | Interpretation |
|-------|---------------|
| 11/11 | Skill is production-ready (v3.1 verified) |
| 10/11 | Minor issue — review the failing test and adjust |
| 8-9/11 | Moderate issues — likely need to adjust SKILL.md or an asset file |
| 6-7/11 | Significant issues — structural problem in the workflow |
| <=5/11 | Major revision needed |

## Version History

| Version | Tests | Changes |
|---------|-------|---------|
| v1.0 | 1-5 | Original test suite |
| v2.0 | 1-8 | Added style profile, error log, consistency checker tests |
| v2.1 | 1-11 | Added Source/Confidence traceability and PLAN gate tests |
| v3.1 | 1-11 | Aligned to 3-phase workflow (GATHER/PLAN/WRITE_AUDIT), fixed file paths |
| v3.2 | 1-11 | Strengthened Source/Confidence traceability in Tests 1-3, 9 |

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

## Version History Update

See "Version History" section above.
