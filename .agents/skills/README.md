# Agent Skills Index

本目录是当前仓库唯一的 Skill 主资产源。所有 Agent 在处理任务前，应先根据本索引选择相关 Skill，再读取对应的 `SKILL.md` 和必要的参考材料。

## 目录原则

- 新增 Skill 统一放在 `.agents/skills/<顶级目录>/<技能目录>/`。
- 每个 Skill 必须包含 `SKILL.md`。
- `SKILL.md` 的 `name` 必须等于 `<顶级目录>-<技能目录>`。
- `SKILL.md` 必须补齐 `metadata.pattern`、`metadata.author`、`metadata.version`。
- `metadata.pattern` 必须等于 `<顶级目录>/<技能目录>`。
- 参考材料放在 `references/`，模板放在 `templates/`，静态模板或表单放在 `assets/`。
- 新增、更新、删除都只在 `.agents/` 下进行。
- 不把 Skill 内容写入 `.cursor/`、`.trae/`、`.qoder/`、`.vscode/` 或根目录 `skills/`。

## 前端负责人架构思考类

| Skill | 入口 | 适用场景 |
| --- | --- | --- |
| frontend-leadership-frontend-leader | `frontend-leadership/frontend-leader/SKILL.md` | 前端负责人管理规划、30+ 团队治理、业务线负责人机制、副手梯队、工程底座、AI 开发治理闭环、前端负责人向产研 AI 协作架构推动者成长 |
| frontend-leadership-org-architect | `frontend-leadership/org-architect/SKILL.md` | 前端组织架构、业务线划分、向上汇报、价值表达、危机处理、组织顶层设计 |
| frontend-leadership-people-culture-manager | `frontend-leadership/people-culture-manager/SKILL.md` | 招聘、面试、绩效、1v1、人才梯队、团队稳定性、临时调动、敏感反馈、高情商沟通 |
| frontend-leadership-tech-efficiency-architect | `frontend-leadership/tech-efficiency-architect/SKILL.md` | 架构、基建、组件库、监控稳定性、AI 效能、质量治理、技术债、AI 驱动产研协作架构与治理、AI 驱动产研组织升级操作系统 |

## 公司公共类

| Skill | 入口 | 适用场景 |
| --- | --- | --- |
| company-public-skill-governance | `company-public/skill-governance/SKILL.md` | Skill 创建规范、目录质量校验、文档归属整理、对话共识建议录入 |
| company-public-wf-openspec-mode | `company-public/wf-openspec-mode/SKILL.md` | AI 落地到真实项目的 OpenSpec/SDD 思路参考、proposal/spec/tasks 机制理解、模型选择；当前 leader 项目不作为强制实践工作流 |

## 更新要求

- 新增、移动、删除 Skill 时，同步更新本索引。
- 修改 Skill 的适用场景时，同步更新根目录 `AGENTS.md` 的常用路由。
- 引用外部仓库内容时，应复制到 `.agents/skills/` 并注明来源或保留原目录结构，不在本仓库保留外部 checkout。
