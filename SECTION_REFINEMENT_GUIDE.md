# Section-Level Refinement 使用指南

> 针对 `paper-methodology` skill 的小节级扩写/重写/校正功能

---

## 功能简介

当你已经完成方法学初稿，但某一节内容不够详细或需要修正时，可以使用 **Section-level refinement mode** 进行局部更新。

**特点**：
- 只更新指定小节，不误改其他章节
- 保持全文术语、符号、编号一致性
- 支持 CN/EN 同步更新

---

## 快速开始（3步走）

### Step 1: 确定目标小节

```
Section 3.2: Loss Function
或
3.2.1: Physics-informed constraint
```

### Step 2: 选择操作类型

| 类型 | 用途 | 场景示例 |
|------|------|----------|
| `expand` | 扩写 | 补充更多实现细节 |
| `rewrite` | 重写 | 结构调整或逻辑优化 |
| `correct` | 校正 | 修复参数值、术语错误 |
| `bilingual-sync` | 中英同步 | 确保 CN/EN 内容对齐 |

### Step 3: 提供输入

使用标准模板：

```markdown
### 输入模板

**target_section_or_subsection**: 3.2

**operation_type**: expand

**existing_section_text_cn**:
3.2 损失函数由重建损失和物理约束损失组成，权重分别设为 1.0 与 0.1。

**existing_section_text_en**:
3.2 The loss function consists of a reconstruction loss and a physics-constraint 
loss, with weights set to 1.0 and 0.1, respectively.

**added_notes**:
- 发现 config 中的物理损失权重实际是 0.25
- 需要补充 KL divergence 正则项的说明

**added_code_or_config_paths**:
- configs/train.yaml
- models/loss.py

**optional_context**: 
上下文：Section 3.1 介绍了模型架构，Section 3.3 将讨论训练策略
```

---

## 完整使用案例

### 案例 1: 扩写实现细节

**场景**：3.2 节特征提取部分太简略，需要补充具体网络结构

```markdown
target_section_or_subsection: 3.2
operation_type: expand

existing_section_text_cn:
3.2 特征提取模块采用双分支结构，分别处理时序监测信号和施工日志文本，随后在共享表示空间中进行融合。

existing_section_text_en:
3.2 The feature extraction module adopts a dual-branch design to process 
time-series monitoring signals and construction-log text, followed by fusion in a 
shared representation space.

added_notes:
- 时序分支：先做 1D convolution (kernel=3, stride=1, padding=1)，再做 temporal attention (8 heads)
- 文本分支：domain vocabulary filtering，去除出现频率 < 5 的词，然后用 BERT-base 编码
- 融合前：两分支输出都经过 layer normalization
- 输出维度：统一映射到 256-dim

added_code_or_config_paths:
- model/fusion_encoder.py  (lines 45-89)
- config/model.yaml
```

**预期输出**：
- MethodSpec 仅更新 Section 3.2 相关字段
- CN/EN 的 3.2 节都扩写为详细版本
- 其他章节保持不变

---

### 案例 2: 校正参数错误

**场景**：发现论文中写的 batch_size 与代码不一致

```markdown
target_section_or_subsection: 3.4.2
operation_type: correct

existing_section_text_cn:
3.4.2 训练采用 Adam 优化器，学习率 0.001，batch size 设为 64，训练 200 个 epoch。

existing_section_text_en:
3.4.2 Training employs the Adam optimizer with a learning rate of 0.001, 
batch size of 64, and 200 epochs.

added_notes:
- 发现论文写的 batch_size=64 是错的
- 实际代码中是 32

added_code_or_config_paths:
- configs/train.yaml  (line 3: batch_size: 32)
```

**预期输出**：
- CN/EN 的 batch_size 都改为 32
- MethodSpec 更新 Source 为 "@configs/train.yaml#L3"
- 其他参数保持不变

---

### 案例 3: 中英同步

**场景**：中文写了新内容，英文需要同步更新

```markdown
target_section_or_subsection: 3.3
operation_type: bilingual-sync

existing_section_text_cn:
3.3 数据预处理包括异常值剔除、缺失值插补和归一化三个步骤。

existing_section_text_en:
3.3 Data preprocessing includes normalization.

added_notes:
- 中文已更新，包含三个步骤
- 英文需要同步补充

added_code_or_config_paths:
- data/preprocess.py
```

**预期输出**：
- 英文 3.3 节扩写为与中文对齐的详细版本
- 术语一致性检查（异常值剔除 → outlier removal）

---

## 注意事项

### ✅ 应该做的

1. **提供现有文本**：给出当前 CN 和 EN 的小节内容，便于保持风格一致
2. **指明代码路径**：即使有 notes，也建议提供代码/config 路径作为 Source
3. **明确操作类型**：根据需求选择合适的 operation_type
4. **检查输出**：确认只有目标小节被修改

### ❌ 避免做的

1. **不提供现有文本**：会导致风格不一致
2. **要求整章重写**：如果只想改一节，不要触发 full-chapter mode
3. **不提供新 Source**：没有新 notes/code 却要求扩写会导致脑补细节
4. **忽略 audit 结果**：TODO/VERIFY 中的警告需要人工确认

---

## 常见错误排查

| 问题 | 原因 | 解决 |
|------|------|------|
| 其他小节也被改了 | 未提供 target_section_or_subsection | 明确指定目标小节 |
| 出现了未提供的参数值 | Source 不足导致脑补 | 补充 code/config 路径 |
| CN/EN 不一致 | operation_type 选错 | 用 bilingual-sync |
| 术语不一致 | 未读取 glossary | 确认读取了 assets/term_glossary.yml |

---

## 版本信息

- Skill Version: v3.7
- 新增功能: Section-level refinement mode
- 测试覆盖: Test 14-15 (regression tests)

---

## 相关文件

- `.opencode/skills/paper-methodology/SKILL.md` - 完整 skill 定义
- `.opencode/commands/methods-bilingual.md` - 命令详细说明
- `.opencode/regression/paper-methodology-tests.md` - 回归测试用例
