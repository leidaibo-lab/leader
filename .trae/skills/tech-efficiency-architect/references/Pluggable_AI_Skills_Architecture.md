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
skills/                        # 根目录
│
├── sztech-frontend/           # 🧑‍💻 第一层：深圳技术部-前端组 (归属前端 TL 审批)
│   │
│   ├── common-skill/          # 🔋 公共 Skill：通用资源聚合大脑 (不再是无生命的目录)
│   │   ├── SKILL.md           # 🧠 指导 AI 如何使用前端全局资源
│   │   ├── references/        # 📚 通用知识：前端全局错误码字典、API 请求规范
│   │   ├── assets/            # 📦 通用模板：前端标准错误弹窗 JSON 格式
│   │   └── scripts/           # ⚙️ 通用脚本：如 fetch-swagger.js (拉取最新接口协议)
│   │
│   ├── checkout-guard/        # 🌟 第二层：具体的独立业务 Skill (收银台防线)
│   │   ├── SKILL.md           # 🧠 大脑指令：可通过相对路径或依赖引用 common-skill 的资源
│   │   └── references/        # 📚 私有知识：仅存放收银台特有的历史 Bug 复盘
│   │
│   └── trade-state-machine/   # 🌟 第二层：具体的独立业务 Skill (交易状态机诊断)
│       ├── SKILL.md
│       └── references/        # 专属知识：交易侧状态机流转图
│
├── sztech-backend/            # ⚙️ 第一层：深圳技术部-后端组 (归属后端 TL 审批)
│   ├── common-skill/          # 🔋 后端公共 Skill (如：全局分库分表规则、微服务契约)
│   │   ├── SKILL.md
│   │   └── references/
│   └── order-state-machine/   # 🌟 第二层：具体的独立业务 Skill
│       └── SKILL.md
│
├── sztech-qa/                 # 🧪 第一层：深圳技术部-测试组 (归属测试 TL 审批)
│   ├── common-skill/          # 🔋 测试公共 Skill
│   │   └── SKILL.md
│   └── perf-report-analyzer/  # 🌟 第二层：具体的独立业务 Skill
│       └── SKILL.md
│
├── product-pm/                # 💡 第一层：产品部 (归属产品总监审批)
│   ├── common-skill/          # 🔋 产品公共 Skill (如：产品黑话字典)
│   │   └── SKILL.md
│   └── prd-generator/         # 🌟 第二层：具体的独立业务 Skill (PRD 生成器)
│       └── SKILL.md           
│
├── operations-ops/            # 📢 第一层：运营部
│   ├── common-skill/
│   │   └── SKILL.md
│   └── content-seo-optimizer/    
│       └── SKILL.md
│
└── company-public/            # 🏢 第一层：公司级公共资产 (架构组/PMO 维护)
    ├── wf-sdd-mode/           # 🌟 第二层：工作流 Skill (SDD 模式插件)
    │   └── SKILL.md       
    └── rules/                 # 第二层：全局规则 (供其他 Skill 挂载)
        ├── react-rules.md     
        └── git-rules.md       
```

---

## 3. 架构优势与落地策略 (产研运协同视角)

### 3.1 优势：完美的权限映射与 Common Skill 的主动赋能
*   **完美的 CODEOWNERS 映射**：物理层面的“部门-职能”文件夹（如 `sztech-frontend`）天然对应了公司里真实的汇报节点。可以直接在根目录配置 `.gitlab/CODEOWNERS` 进行精准的细粒度权限管控。
*   **Common Skill 变被动为主动**：将 `common/` 升级为 `common-skill`，意味着通用资源不再是躺在目录里等待被读取的死文件。它拥有了自己的 `SKILL.md`，可以主动指导 AI：“我是前端的公共大脑，当你处理网络请求错误时，请必须参考我的 `references/error-codes.md`”。
*   **视觉与心智的双重减负**：IDE 按字母排序，所有 `sztech-` 依然聚在一起。日常开发时，前端工程师视野完全聚焦在 `sztech-frontend`，没有任何嵌套地狱，只有纯粹的业务 Skill 和公共 Skill 协同工作。

### 3.2 落地策略：跨职能的化学反应与工作流解耦
当深圳技术部的一名前端员工开发“交易侧状态机”需求时：
1. 他向 AI 提问：“我要用 SDD 模式基于产品部的最新 PRD，修改交易状态机代码”。
2. AI 自动组合跨职能路径：让 `@skills/sztech-frontend/trade-state-machine`（查前端私有逻辑，并自动联动 `@skills/sztech-frontend/common-skill` 获取通用知识），去读取 `@skills/company-public/rules/react-rules.md`（查代码规范），最后用 `@skills/company-public/wf-sdd-mode`（工作流插件）输出。
3. 工作流（SDD）与业务防线（状态机逻辑）彻底解耦，哪怕未来淘汰 SDD 模式，深圳前端沉淀的业务资产分毫不损。
