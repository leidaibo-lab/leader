---
name: "company-public-wf-openspec-mode"
description: "OpenSpec/SDD 思路参考。用于前端负责人理解 AI 如何落地到真实项目流程、评估 proposal/spec/tasks/review 等机制，不作为当前 leader 项目的强制实践工作流。"
metadata:
  pattern: "company-public/wf-openspec-mode"
  author: "company-public"
  version: "0.1.0"
---

# OpenSpec/SDD 思路参考

> **设计哲学**：业务知识是核心资产，工作流是可替换外壳。本 Skill 在当前 leader 项目中只作为负责人理解 AI 落地到项目流程的参考模型，不要求在本项目生成完整 proposal/spec/tasks/review 资产。

## 适用范围

| 场景 | 当前项目处理方式 | 说明 |
|---|---|---|
| 负责人规划 AI 落地路径 | ✅ 参考 | 用于理解 SDD 如何约束 AI 研发流程 |
| 讨论 proposal/spec/tasks/review 机制 | ✅ 参考 | 输出方案、判断边界、拆解价值，不强制生成文件 |
| 当前 leader 项目文档整理 | ❌ 不启用实践流 | 直接沉淀到 Skill / references 即可 |
| 真实业务项目复杂变更 | ⚠️ 可借鉴 | 需要在业务项目内另行补齐模板、校验器和团队执行约定 |

## 参考工作流

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

## 5 + 2 静态约束参考

### 核心 5 条（真实业务项目可考虑）

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

## 当前项目 AI 行为指令

当 AI 在当前 leader 项目中讨论 OpenSpec/SDD 时：

1. 只把 OpenSpec/SDD 作为 AI 落地到真实项目流程的参考框架。
2. 不要求在当前项目创建完整 `specs/`、`tasks.md`、`review.md` 或 validator。
3. 如果用户明确要求在业务项目实践，再根据目标项目补齐 `templates/spec.md`、`templates/tasks.md` 和校验器。
4. 输出时重点解释负责人需要理解的价值：需求契约、任务拆解、验证前置、Review 留痕、归档复盘。
5. 不把当前 leader 项目的 Skill 资产整理误判为 OpenSpec 执行流。

## 反向使用（当 AI 不该启用本 Skill 时）

明确禁用本 Skill 的场景：
- 当前 leader 项目中普通 Skill / reference 整理。
- 设计系统/UI Kit 的视觉迭代（snapshot 测试已足够）
- 营销活动页/落地页（生命周期短，测试成本 > 收益）
- 文档/注释/类型定义的纯编辑改动

> AI 在以上场景应明确告知用户："当前不需要套 OpenSpec/SDD 实践流，直接按项目 Skill 归属沉淀即可"。

## 治理与版本

- 本 Skill 当前由负责人规划视角维护，只保留 SDD/OpenSpec 的方法参考。
- 若未来要在真实业务项目落地，应迁移为业务项目内的可执行工作流，并补齐模板、校验器和执行约定。
