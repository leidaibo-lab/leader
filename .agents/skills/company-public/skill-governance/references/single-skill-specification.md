# Single AI Skill Design Specification (单体 Skill 设计规范)

在【公司-部门-团队】的组织级 AI 资产架构下，为了确保单个 AI Skill 能够**独立演进、高度复用、且不与任何特定开发模式（如 SDD）强绑定**，每一个 Skill 必须严格遵循以下内部结构与编写规范。

## 1. 标准目录结构 (Micro-package 模式)

每一个 Skill 都被视为一个独立的“微型能力包”，其内部目录必须且只能包含以下结构：

```text
[skill-name]/                   # Skill 名称 (使用连字符，如 promotion-guard)
├── SKILL.md                    # 🌟 核心大脑：Prompt 指令 (必须包含 Frontmatter)
├── references/                 # 📚 强内聚知识库：只存放与本 Skill 核心职责相关的业务知识
│   ├── [domain-rules].md       # 例如：降级熔断规则说明、特定业务域术语表
│   └── post-mortems/           # 历史 P0 故障复盘报告 (极具价值的防坑指南)
├── assets/                     # 📦 静态资产：本 Skill 专属的 JSON/图片等模板
└── scripts/                    # ⚙️ 动态脚本 (可选)：执行前需要拉取实时数据的 Node/Python 脚本
```

**红线规定**：
`references/` 目录下**绝对不允许**存放全公司通用的工程规范（如 React 编码规范）或部门级的通用资源。
- 公司级规范必须收敛在 `.agents/skills/company-public/rules/` 中。
- 部门级通用资源必须收敛在对应顶级目录的公共 Skill 中（如 `.agents/skills/frontend-leadership/frontend-leader/` 或未来新增的 `<部门>/<common-skill>/`）。

## 2. SKILL.md 编写范式：面向接口与组装 (Stateless & Composable)

`SKILL.md` 的编写必须将“核心业务逻辑”与“输出模式/工作流”彻底解耦。

### 2.1 必选结构模板

```markdown
---
name: [skill-name]
description: [简短的一句话描述，说明在什么场景下调用该专家]
---

# 角色定位 (Role)
[描述该 Skill 代表的虚拟专家角色，如“电商大促保障专家”或“AB实验分析师”。]

# 核心诊断/执行逻辑 (Core Stateless Logic)
[纯粹的能力描述，不夹杂任何特定模式的输出要求。例如：]
当你审查代码时，必须严格检查：
1. 异步请求是否被 try-catch 妥善包裹？
2. 是否有防抖处理？

# 业务上下文挂载 (Domain Knowledge Injection)
[明确要求 AI 读取 `references/` 下的特定文件。例如：]
在执行前，你必须主动读取本目录下的 `references/fallback-rules.md`，基于里面的错误码映射表来判断代码的准确性。

# 🚨 工作流适配接口 (Workflow Adapter)
[这是实现可插拔的核心。声明如何根据用户的上下文改变输出格式。例如：]
1. **全局规范遵循**：请结合 `.agents/skills/company-public/rules/` 来规范你的代码输出。
2. **工作流输出 (如 SDD)**：
   - **如果**用户处于 SDD/OpenSpec 工作流中，请结合 `.agents/skills/company-public/wf-openspec-mode` 规范你的输出。
   - **如果**未指定工作流，请直接使用 Markdown 列表输出你的核心诊断结论。
```

## 3. 设计优势分析

1. **彻底解耦 SDD 等流行模式**：如果未来 SDD 模式被淘汰，只需要修改 `SKILL.md` 中的【工作流适配接口】段落。Skill 积累的核心业务知识（如历史复盘报告）分毫未损。
2. **防腐化 (Anti-corruption)**：通过将业务黑话锁定在 `references/`，全局规范锁定在公共规则中。Skill 变成了一个干净的纯逻辑处理节点。
3. **极简复用**：当业务线需要组合新的能力时，就像搭乐高积木一样，将不同的 Skill 叠加调用即可。
