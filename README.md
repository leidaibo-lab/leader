# Leader

这是一个面向前端团队负责人工作的知识资产仓库，用来沉淀团队治理、组织架构、人才培养、技术效能、AI 协作治理和阶段性输出物。

本仓库不是业务代码项目，核心资产是 `.agents/skills/` 下的可复用 Skill，以及 `outputs/` 下的文档化产出。

## 目录结构

```text
.
├── AGENTS.md
├── README.md
├── .agents/
│   └── skills/
│       ├── README.md
│       ├── company-public/
│       └── frontend-leadership/
└── outputs/
```

## 核心入口

- `AGENTS.md`：Agent 协作规则、中文输出要求、提交规范和常用 Skill 路由。
- `.agents/skills/README.md`：本仓库 Skill 索引，处理任务前优先读取。
- `.agents/skills/frontend-leadership/`：前端负责人相关的组织、人才、技术和管理方法。
- `.agents/skills/company-public/`：公司级公共流程、Skill 治理和 OpenSpec 工作流。
- `outputs/`：阶段性文档、图示、标准草案和个人成长记录模板。

## Skill 分类

### 前端负责人架构思考类

- `frontend-leadership/frontend-leader`：团队治理、业务线负责人机制、工程底座、AI 开发治理闭环。
- `frontend-leadership/org-architect`：组织架构、业务线划分、向上汇报、价值表达和组织顶层设计。
- `frontend-leadership/people-culture-manager`：招聘、面试、1v1、绩效、人才梯队和团队稳定性。
- `frontend-leadership/tech-efficiency-architect`：架构、基建、组件库、监控稳定性、AI 效能和质量治理。

### 公司公共类

- `company-public/skill-governance`：Skill 创建规范、目录质量校验和文档归属整理。
- `company-public/wf-openspec-mode`：OpenSpec/SDD 工作流、proposal/spec/tasks 和模型选择。

## 使用方式

处理任何任务前，先按以下顺序读取上下文：

1. 查看 `git status`、`git diff --stat`、`git diff --name-status`，确认本次变更范围。
2. 读取 `AGENTS.md`，确认协作规则和提交规范。
3. 读取 `.agents/skills/README.md`，选择当前任务需要的 Skill。
4. 读取对应 Skill 的 `SKILL.md`。
5. 如 `SKILL.md` 指向 `references/`、`templates/` 或 `assets/`，只读取与当前任务相关的材料。

## 维护规则

- 新增或更新 Skill 只修改 `.agents/skills/`。
- Skill 路径必须符合 `.agents/skills/<顶级目录>/<技能目录>/SKILL.md`。
- `SKILL.md` 的 `name` 必须等于 `<顶级目录>-<技能目录>`。
- `metadata.pattern` 必须等于 `<顶级目录>/<技能目录>`。
- 新增、移动或删除 Skill 时，同步更新 `.agents/skills/README.md`。
- 修改常用 Skill 路由时，同步更新 `AGENTS.md`。
- 不在仓库内维护 `.cursor/`、`.trae/`、`.qoder/`、`.vscode/`、根目录 `skills/` 等 IDE 或外部 checkout 目录。

## 提交规范

提交信息遵守：

```text
type(scope): message
```

示例：

```text
docs(readme): 补充项目入口说明
```
