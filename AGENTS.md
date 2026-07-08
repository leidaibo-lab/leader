# AGENTS.md

## 基本协作规则

- 使用中文输出。
- 通过变更检索出关键变更信息，先看 `git status`、`git diff --stat`、`git diff --name-status`，再判断本次整理或实现范围。
- 遵守项目 Git 提交规范：`type(scope): message`。
- 不依赖具体 IDE 的 Skill 自动识别；所有 Agent 都必须主动读取本文件和 `.agents/skills/README.md`。

## Skill 主目录

- 本仓库所有可复用 Skill、规则、模板和参考材料统一收敛到 `.agents/skills/`。
- `.agents/skills/` 是唯一主资产源。新增或更新 Skill 时，只修改该目录。
- Skill 遵守两级目录：`.agents/skills/<顶级目录>/<技能目录>/SKILL.md`。
- `SKILL.md` 的 `name` 必须等于 `<顶级目录>-<技能目录>`，并补齐 `metadata.pattern`、`metadata.author`、`metadata.version`。
- 不在仓库内维护 `.cursor/`、`.trae/`、`.qoder/`、`.vscode/`、根目录 `skills/` 这些 IDE 或外部 checkout 目录。
- 如果确实需要 IDE 适配，也应由本地环境临时生成，不能反向进入仓库。

## Agent 使用流程

1. 先读取 `.agents/skills/README.md`，判断当前任务需要使用哪些 Skill。
2. 再读取对应 Skill 的 `SKILL.md`。
3. 如果 `SKILL.md` 指向 `references/`、`assets/`、`templates/`，只读取与当前任务相关的文件。
4. 输出时优先复用 Skill 中沉淀的口径、模板、清单和案例，不要重新发散一套说法。
5. 如果新增了 Skill 或引用文件，同步更新 `.agents/skills/README.md` 的索引和适用场景。
6. 规划、架构、管理方法论类讨论中，如果形成可复用共识，应主动给出“建议录入”清单；用户确认后，再写入对应 Skill。

## 常用 Skill 路由

- 前端团队负责人规划、30+ 团队治理、业务线负责人机制、AI 开发治理闭环、前端负责人向产研 AI 协作架构推动者成长：读取 `.agents/skills/frontend-leadership/frontend-leader/SKILL.md`。
- 前端组织架构、业务线划分、向上汇报、组织顶层设计：读取 `.agents/skills/frontend-leadership/org-architect/SKILL.md`。
- 招聘、面试、绩效、1v1、人才梯队、团队稳定性：读取 `.agents/skills/frontend-leadership/people-culture-manager/SKILL.md`。
- 架构、基建、组件库、监控稳定性、AI 效能、质量治理、AI 驱动产研协作架构与治理、AI 驱动产研组织升级操作系统：读取 `.agents/skills/frontend-leadership/tech-efficiency-architect/SKILL.md`。
- Skill 创建规范、目录质量校验、前端负责人文档归属整理、对话共识建议录入：读取 `.agents/skills/company-public/skill-governance/SKILL.md`。
- AI 落地到真实项目的 OpenSpec/SDD 思路、proposal/spec/tasks 机制理解、模型选择：读取 `.agents/skills/company-public/wf-openspec-mode/SKILL.md`；当前 leader 项目不作为强制实践工作流。
