---
name: "company-public-skill-governance"
description: "公司级 Skill 创建与治理规范。用于校验 .agents/skills 下 Skill 是否符合 seakoi/skills 风格的两级目录、命名、metadata、中文正文、引用归属和前端负责人架构思考类文档归档要求。"
metadata:
  pattern: "company-public/skill-governance"
  author: "company-public"
  version: "0.1.0"
---

# Skill 治理规范

## 核心规则

- 所有 Skill 只放在 `.agents/skills/`。
- 目录采用两级结构：`<顶级目录>/<技能目录>/SKILL.md`。
- `name` 必须等于 `<顶级目录>-<技能目录>`。
- frontmatter 必须包含 `name`、`description`、`metadata.pattern`、`metadata.author`、`metadata.version`。
- `metadata.pattern` 必须等于 `<顶级目录>/<技能目录>`。
- 正文以中文为主，保留必要英文术语可以，但不要让英文成为主体。
- 详细资料放 `references/`，模板放 `templates/`，可复用静态表单或附件放 `assets/`。

## 前端负责人文档归属

- 团队治理、业务线负责人、个人/团队成长证据、交付责任留底：归入 `frontend-leadership/frontend-leader`。
- 组织架构、业务线划分、业务线负责人执行标准、公司交付视角：归入 `frontend-leadership/org-architect`。
- 招聘、面试、1v1、绩效、人才梯队、人员调动稳定性：归入 `frontend-leadership/people-culture-manager`。
- 架构、基建、AI 效能、组件库、监控稳定性、基础资产推广：归入 `frontend-leadership/tech-efficiency-architect`。
- Skill 目录规范、单体 Skill 设计、可插拔 Skill 架构：归入 `company-public/skill-governance`。
- OpenSpec、SDD、模型选择、proposal/spec/tasks 工作流：归入 `company-public/wf-openspec-mode`。

## 更新要求

- 新增、更新、删除都只在 `.agents/` 下进行。
- 修改任一 Skill 路径、名称或适用场景后，同步更新 `.agents/skills/README.md` 和根目录 `AGENTS.md`。
- 不新增 `.cursor/`、`.trae/`、`.qoder/`、`.vscode/`、根目录 `skills/`。
