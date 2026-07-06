# AI Skill Repository Architecture: Pluggable & Domain-Driven Design

## 1. 核心设计理念：升维至组织与业务线 (Organization-Driven Design)

随着团队规模扩展至 30+ 人，我们不能仅仅把 AI 资产当成“前端程序员修 Bug 的工具”。如果按“代码审查”、“写测试”来划分，只是在复刻通用的 AI 工具；只有**按公司真实的组织架构和业务线来划分**，才能打造公司专属的数字资产护城河。

核心原则：
1. **面向组织节点，而非单一角色**：Skill 应该代表某个业务域的“数字员工”（如：电商订单链路专家、大促保障专家），而不是局限于某个动作。
2. **跨职能上下文融合**：一个业务线 Skill 的上下文中，应包含产品 PRD、后端接口契约和 QA 用例，打破前端单一视角的局限。
3. **彻底解耦开发模式**：业务领域知识（如电商规则）是核心资产，而开发模式（如 SDD、TDD）只是随时可替换的“工作流外壳”。

---

## 2. 终极演进：部门职能混合架构 (Hybrid Two-Layer Architecture)

遵循**康威定律（Conway's Law）**结合公司真实阵型（130+ 人：运营、产品、深圳技术部、南京西舟鲤）。

在经历了深层嵌套与极限拍平的推演后，我们找到了物理隔离与极简认知的黄金分割点：**将【部门】与【职能】合并为一层物理目录**。在这一层内部，我们将以往静态的共享目录升级为主动的 **公共 Skill (Common Skill)**，实现了通用资源的智能化聚合与分发。

整个仓库的有效物理深度被死死锁定在 **2 层**：

```text
.agents/skills/                              # Skill 主目录
│
├── frontend-leadership/                     # 第一层：前端负责人治理域
│   │
│   ├── frontend-leader/                     # 前端负责人管理规划
│   │   ├── SKILL.md
│   │   └── references/
│   │
│   ├── org-architect/                       # 组织架构与业务线治理
│   │   ├── SKILL.md
│   │   └── references/
│   │
│   ├── people-culture-manager/              # 招聘、绩效、梯队、稳定性
│   │   ├── SKILL.md
│   │   ├── references/
│   │   └── assets/
│   │
│   └── tech-efficiency-architect/           # 架构、基建、AI、质量
│       ├── SKILL.md
│   │   └── references/
│
└── company-public/                          # 🏢 第一层：公司级公共资产 (架构组/PMO 维护)
    ├── skill-governance/                    # Skill 创建与治理规范
    │   ├── SKILL.md
    │   └── references/
    ├── wf-openspec-mode/                    # OpenSpec/SDD 思路参考
    │   └── SKILL.md       
```

---

## 3. 架构优势与落地策略 (产研运协同视角)

### 3.1 优势：完美的权限映射与 Common Skill 的主动赋能
*   **完美的 CODEOWNERS 映射**：物理层面的“领域-能力”文件夹（如 `frontend-leadership`）天然对应真实责任边界。可以直接配置 CODEOWNERS 进行精准的细粒度权限管控。
*   **Common Skill 变被动为主动**：将 `common/` 升级为 `common-skill`，意味着通用资源不再是躺在目录里等待被读取的死文件。它拥有了自己的 `SKILL.md`，可以主动指导 AI：“我是前端的公共大脑，当你处理网络请求错误时，请必须参考我的 `references/error-codes.md`”。
*   **视觉与心智的双重减负**：所有前端负责人治理材料聚合在 `frontend-leadership`，公共治理材料聚合在 `company-public`，没有 IDE 私有目录和外部 checkout 干扰。

### 3.2 落地策略：跨职能的化学反应与工作流解耦
当前需要整理“30+ 前端团队架构治理和线上闭环”时：
1. 先读取 `.agents/skills/company-public/skill-governance/SKILL.md` 判断文档归属。
2. 再按问题性质读取 `.agents/skills/frontend-leadership/org-architect` 或 `.agents/skills/frontend-leadership/tech-efficiency-architect`。
3. 如果涉及 AI 如何落地到真实业务项目的 SDD/OpenSpec 思路，再参考 `.agents/skills/company-public/wf-openspec-mode`；当前 leader 项目不在本仓库执行完整工作流。
4. 工作流可以替换，但前端负责人治理知识资产保持在 `frontend-leadership` 下稳定演进。
