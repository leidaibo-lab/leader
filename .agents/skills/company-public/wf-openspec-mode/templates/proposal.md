# Proposal: <change-name>

## 元信息 [必填]

- **type**: <feature | bugfix | refactor | chore>
- **scope**: <单模块 | 跨模块 | 架构级>
- **size**: <S (<50 行) | M (<500 行) | L (≥500 行)>
- **owner**: <负责人>
- **reviewers**: <Stage1 reviewer> / <Stage2 reviewer>

## 1. 背景与动机 [必填]

为什么要做这个变更？解决的真实问题是什么？

## 2. 目标 (Goals)

- 必达目标 1
- 必达目标 2

## 3. 非目标 (Non-Goals) [防 Scope Creep]

明确不做什么，避免实现期失控。

- 本次不处理 X
- 本次不优化 Y

## 4. 影响面分析

| 维度 | 影响 |
|---|---|
| 用户可见行为 | <是/否，具体说明> |
| 接口契约 | <破坏性变更？> |
| 数据存储 | <schema 变化？> |
| 性能 | <预估影响> |
| 安全 | <新增攻击面？> |

## 5. 风险与回滚

- **主要风险**：
- **回滚方法**：
- **灰度策略**（如适用）：

## 6. 验收标准（指向 spec.md）

详见 `specs/spec.md` 的 BDD 场景与 DoD。
