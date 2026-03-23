# Skill Triggering Prompt Set

这套文件模仿 `superpowers/tests/skill-triggering/prompts` 的组织方式。

目录说明：

- `prompts/trigger-*.txt`：应当触发复杂任务流程
- `prompts/no-trigger-*.txt`：不应触发复杂任务流程
- `prompts/borderline-*.txt`：边界案例，重点看判断是否稳定

使用方式：

1. 逐条把 `prompts/` 下的内容当作用户输入喂给模型
2. 观察是否正确触发 `openclaw-cn-model-guardrails`
3. 记录是否误触发、漏触发、或边界判断不稳

建议结合 [trigger-samples.md](../trigger-samples.md) 一起看，那里有更完整的预期说明。

## 当前覆盖

### 应触发

- `trigger-001.txt`
- `trigger-002.txt`
- `trigger-003.txt`
- `trigger-004.txt`

### 不应触发

- `no-trigger-001.txt`
- `no-trigger-002.txt`
- `no-trigger-003.txt`
- `no-trigger-004.txt`

### 边界案例

- `borderline-001.txt`
- `borderline-002.txt`
- `borderline-003.txt`

## 简单判定规则

- 简单、单轮、低风险任务：不触发
- 多步骤、需确认、需持续推进、易提前结束任务：触发
- 边界案例：看是否真的需要步骤清单、理解确认和完成前验收
