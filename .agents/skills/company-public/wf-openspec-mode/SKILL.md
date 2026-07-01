---
name: "company-public-wf-openspec-mode"
description: "OpenSpec 工作流外壳（融合 Superpowers 静态约束）。当用户使用 /opsx:propose、/opsx:apply、/opsx:archive 或进行 spec 驱动开发时调用。前端团队默认开启，后端/跨端可选。"
metadata:
  pattern: "company-public/wf-openspec-mode"
  author: "company-public"
  version: "0.1.0"
---

# OpenSpec 工作流模式（融合版）

> **设计哲学**：业务知识是核心资产，工作流是可替换外壳。本 Skill 是"外壳"——
> 它把 Superpowers 中**5 条最有价值的静态约束**固化进 OpenSpec 的产出物，
> 让全员零额外学习成本拿到 80% 的 Superpowers 价值。

## 适用范围

| 场景 | 是否启用 | 说明 |
|---|---|---|
| 纯前端开发（≥ S 级变更） | ✅ 默认开启 | 全员标准流程 |
| 前端 hotfix（< 50 行） | ⚠️ 仅启用 review.md | 轻量路径 |
| 前端 POC / A/B 实验 | ❌ 不启用 | 抛弃式代码无需流程 |
| 跨端 / 全栈复杂模块 | ✅ 开启 + 叠加 Superpowers | 由 TL 决定 |

## 核心工作流

```text
/opsx:propose <idea>
   ↓
   ├─ 生成 proposal.md         ← 契约层
   ├─ 生成 specs/spec.md       ← 含 DoD 字段（约束 ④）
   └─ 生成 tasks.md            ← 含原子性 + 测试前置（约束 ① ②）

/opsx:apply
   ↓
   ├─ 按 tasks.md 顺序执行
   └─ 每个 [VERIFY] 任务自动跑 validator

   [若 type=bugfix] → 强制要求 bugfix-hypothesis.md（约束 ⑤）

   ↓
   生成 review.md（约束 ③：双阶段 review）
   ↓
   anti-pattern 自检（增强约束 ⑥）

/opsx:archive
   ↓
   validator 全量校验 → 通过则归档
```

## 5 + 2 静态约束清单

### 核心 5 条（必启用）

| # | 约束名 | 源 Superpowers Skill | 落地文件 | 强制度 |
|---|---|---|---|---|
| ① | 任务原子性 | `writing-plans` | `tasks.md` | 强制 |
| ② | 测试前置 | `test-driven-development`（轻量） | `tasks.md` | 强制 |
| ③ | 双阶段 Review | `requesting-code-review` | `review.md` | 强制 |
| ④ | 完成定义 (DoD) | `verification-before-completion` | `spec.md` | 强制 |
| ⑤ | 调试 4-Phase | `systematic-debugging` | `bugfix-hypothesis.md` | 条件强制（仅 bugfix） |

### 增强 2 条（推荐启用）

| # | 约束名 | 源 Superpowers Skill | 落地文件 | 强制度 |
|---|---|---|---|---|
| ⑥ | Anti-Pattern 自检 | `using-superpowers` | `references/anti-patterns.md` | 推荐 |
| ⑦ | Review 反馈留痕 | `receiving-code-review` | `review.md`（反馈表） | 推荐 |

## AI 行为指令

当 AI 在 OpenSpec 流程中工作时，必须：

1. **生成 proposal 时**：自动套用 `templates/proposal.md`，识别 type 字段（feature/bugfix/refactor）
2. **生成 spec 时**：自动套用 `templates/spec.md`，强制填充 `## 2. 完成定义 (DoD)` section
3. **生成 tasks 时**：自动套用 `templates/tasks.md`，遵守"原子性 + 测试前置"双约束
4. **bugfix 类型**：额外生成 `bugfix-hypothesis.md`，4 个 Phase 全部填写
5. **archive 前**：自动跑 `validators/superpowers-constraints.js`，任何一项不通过则阻止归档
6. **遇到偏离 spec 的实现**：必须先回写 `specs/spec.md`，再继续

## 反向使用（当 AI 不该启用本 Skill 时）

明确禁用本 Skill 的场景：
- 设计系统/UI Kit 的视觉迭代（snapshot 测试已足够）
- 营销活动页/落地页（生命周期短，测试成本 > 收益）
- 文档/注释/类型定义的纯编辑改动

> AI 在以上场景应明确告知用户："此变更建议绕过 OpenSpec 流程，直接 commit"。

## 治理与版本

- 本 Skill 由**架构组**维护，业务团队不得直接修改 `templates/` 与 `validators/`
- 上游 Superpowers 升级时，季度评审 → 决定是否同步更新约束
- 约束源映射详见 `references/constraint-mapping.md`
