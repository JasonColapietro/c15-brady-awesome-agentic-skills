# Awesome Agentic Skills 知识库

> 一份跨平台、跨工具的 AI Agent Skills 精选合集
> 涵盖 Claude Code · Cursor · Windsurf · GitHub Copilot · Devin · Codex CLI · Gemini CLI · 等主流 AI 编程助手

---

## 📖 目录

- [一、生态概览](#一生态概览)
- [二、各平台配置文件对照](#二各平台配置文件对照)
- [三、决策矩阵：该用哪种机制？](#三决策矩阵该用哪种机制)
- [四、各平台快速上手](#四各平台快速上手)
  - [4.1 Claude Code](#41-claude-code)
  - [4.2 Cursor](#42-cursor)
  - [4.3 Windsurf](#43-windsurf)
  - [4.4 GitHub Copilot](#44-github-copilot)
- [五、Claude Code Skills 大全](#五claude-code-skills-大全)
  - [5.1 官方核心 Skills（15 个）](#51-官方核心-skills15-个)
  - [5.2 Superpowers 系列（14 个）](#52-superpowers-系列14-个)
  - [5.3 Example Skills（14 个）](#53-example-skills14-个)
  - [5.4 社区精选 Skills（14 个）](#54-社区精选-skills14-个)
- [六、Cursor Rules & Skills](#六cursor-rules--skills)
- [七、Windsurf Rules & Skills](#七windsurf-rules--skills)
- [八、GitHub Copilot Instructions](#八github-copilot-instructions)
- [九、跨平台一站式方案](#九跨平台一站式方案)
- [十、大型 Awesome 合集仓库](#十大型-awesome-合集仓库)
- [十一、知名企业官方 Skills](#十一知名企业官方-skills)
- [十二、按领域分类的 Skills](#十二按领域分类的-skills)
- [十三、CLAUDE.md 模板（可直接用）](#十三claudemd-模板可直接用)
- [十四、Agent Skills 最佳实践](#十四agent-skills-最佳实践)
- [十五、常见陷阱 & 避坑指南](#十五常见陷阱--避坑指南)
- [十六、快速入门推荐清单](#十六快速入门推荐清单)
- [十七、参考链接汇总](#十七参考链接汇总)

---

## 一、生态概览

| 平台 | 规则机制 | Skills 目录 | 加载方式 |
|------|----------|------------|----------|
| **Claude Code** | `CLAUDE.md` + `.claude/rules/` | `.claude/skills/*/SKILL.md` | 按需触发（description 匹配） |
| **Cursor** | `.cursorrules` / `.cursor/rules/*.mdc` | `.cursor/skills/` | 全局匹配 + Auto Attached |
| **Windsurf** | `.windsurfrules` / `.windsurf/rules/` | `.windsurf/skills/` | 按规则文件 glob 匹配 |
| **GitHub Copilot** | `.github/copilot-instructions.md` | `.github/instructions/*.instructions.md` | 会话注入 |
| **Codex CLI** | `CLAUDE.md` + rules | `.claude/skills/` | 按需加载 |
| **Gemini CLI** | `GEMINI.md` + rules | `.gemini/skills/` | 按需加载 |
| **AGENTS.md** | `AGENTS.md`（开放标准） | 跨平台统一 | 60k+ 项目已采用 |

---

## 二、各平台配置文件对照

| 配置文件 | 支持平台 | 说明 |
|----------|---------|------|
| `CLAUDE.md` | Claude Code, Codex CLI | 项目级指令，会话开始自动加载 |
| `.claude/rules/*.md` | Claude Code | 路径作用域规则，触及时加载 |
| `.claude/skills/*/SKILL.md` | Claude Code, Codex, Gemini CLI | 按 name/description 匹配触发 |
| `.claude/agents/*.md` | Claude Code | 子智能体定义 |
| `.cursorrules` | Cursor（旧版） | 项目级指令 |
| `.cursor/rules/*.mdc` | Cursor（新版 Project Rules） | 基于 glob 自动附加 |
| `.windsurfrules` | Windsurf | 项目级指令 |
| `.windsurf/rules/*.md` | Windsurf | 规则文件 |
| `.windsurf/skills/` | Windsurf | Skills 目录 |
| `.github/copilot-instructions.md` | GitHub Copilot | 主指令文件 |
| `.github/instructions/*.instructions.md` | GitHub Copilot | 分领域指令 |
| `AGENTS.md` | Copilot, Codex, Cursor, Devin 等 20+ | Linux Foundation 开放标准 |
| `GEMINI.md` | Gemini CLI | Google 版 CLAUDE.md |

---

## 三、决策矩阵：该用哪种机制？

> **"Claude 该知道的写 CLAUDE.md，必须发生的写 Hook，反复照做的做 Skill，不想污染主上下文的给 Subagent"**

| 场景 | 推荐机制 | 为什么 |
|------|---------|--------|
| 项目技术栈、构建命令、编码规范 | **CLAUDE.md** | 每次会话自动加载，全局可用 |
| 特定目录/文件的专属规范 | **Rules**（路径规则） | 按路径匹配触发，不浪费上下文 |
| 部署流程、测试步骤、代码审查清单 | **Skills** | description 匹配才加载，按需使用 |
| 独立视角审查代码、探索大型代码库 | **Subagents** | 独立上下文，不占主会话预算 |
| 提交前强制 lint、阻止密钥泄露 | **Hooks** | 硬性机制，模型无法绕过 |
| 需要实时外部数据（GitHub、DB、API） | **MCP Servers** | 工具调用，实时读写 |

**经验法则：**
- 每周用 3 次以上 → **做成 Skill**
- 整个项目都要知道 → **放 CLAUDE.md**
- 必须执行不能商量 → **写 Hook**
- 一次性复杂探索 → **开 Subagent**

---

## 四、各平台快速上手

### 4.1 Claude Code

```bash
# 项目级（推荐团队共用）
mkdir -p .claude/skills/<skill-name>
# 放入 SKILL.md

# 用户级（个人全局可用）
mkdir -p ~/.claude/skills/<skill-name>

# 安装 Superpowers（obra 市场）
claude add superpowers

# 检查技能和上下文预算
/doctor
```

### 4.2 Cursor

```bash
# 新版 Project Rules（推荐）
mkdir -p .cursor/rules
# 创建 .cursor/rules/<name>.mdc（YAML frontmatter + Markdown）

# 旧版单文件
# 项目根目录放 .cursorrules

# Skills 目录（Cursor 0.45+）
mkdir -p .cursor/skills/<skill-name>
```

**.mdc 规则文件示例：**
```yaml
---
description: React 组件编写规范
globs: "src/components/**/*.tsx"
---
# React 组件规范
- 使用函数式组件 + Hooks
- Props 用 interface 定义并导出
- 每个组件一个文件
```

### 4.3 Windsurf

```bash
# 项目级主指令
echo "your rules here" > .windsurfrules

# 分文件规则 / Skills / Agents
mkdir -p .windsurf/{rules,skills,agents}
```

### 4.4 GitHub Copilot

```bash
# 主指令
mkdir -p .github && echo "instructions" > .github/copilot-instructions.md

# 分领域指令
mkdir -p .github/instructions
# 放入 *.instructions.md 文件
```

> **注意：** Copilot 优先读取 `AGENTS.md`（如果存在），其次才是 `copilot-instructions.md`

---

## 五、Claude Code Skills 大全

### 5.1 官方核心 Skills（15 个）

Anthropic 官方团队出品，质量最高、维护最活跃。

| Skill | 功能说明 | 典型使用场景 |
|-------|---------|-------------|
| **claude-api** | Claude API/Anthropic SDK 的完整参考手册。当你需要查询模型 ID、定价、参数配置、流式传输、工具调用、MCP 集成、缓存策略等信息时，它会给出经过验证的最新答案 | 开发 AI 应用时查 API 用法、算 token、排错 |
| **code-review** | 对当前工作区 diff 进行代码审查，检查 bug、可重用性、效率、代码简化等方面的问题。提供修改建议而非直接修改 | 提交代码前做一次完整的 diff-level review |
| **deep-research** | 多源深度研究引擎。自动搜索网络、抓取内容、对抗验证事实，然后合成一份带引用的研究报告 | 做技术选型调研、竞品分析、学习新框架 |
| **verify** | 端到端验证。运行你的应用/脚本，执行受影响的操作流程，观察实际行为来判断代码改动是否正确 | 改完核心逻辑后确保功能正常，比跑单元测试更全面 |
| **simplify** | 代码审查 + 自动修复。审查当前 diff 中可重用、可简化、可提升效率的地方，并自动应用修改 | 重构代码、减少重复、提升性能 |
| **security-review** | 安全漏洞审查。检查代码中的 SQL 注入、XSS、CSRF、认证绕过、敏感信息泄露等安全问题 | 上线前的安全检查、处理安全工单 |
| **run** | 自动检测项目类型并启动应用，然后你可以观察改动效果 | 确认 UI 改动是否生效、调试运行时问题 |
| **init** | 根据项目描述自动初始化项目结构、配置文件、安装依赖 | 快速搭建新项目脚手架 |
| **review** | 通用代码审查 Skill，审查任意变更或指定文件 | diff review 之外的代码审查需求 |
| **dataviz** | 数据可视化全套方案。自动选择合适的图表类型、配色方案（含色板校验工具），生成美观的图表 | 做数据分析报告、生成仪表盘 |
| **update-config** | 管理 Claude Code 配置。修改 settings.json 中的权限、主题、模型等设置 | 添加命令白名单、切换模型 |
| **loop** | 定时循环执行任务。支持 `/loop 5m /code-review` 等格式 | 持续监控构建状态、定时检查 |
| **fewer-permission-prompts** | 扫描你的常用命令，生成权限白名单加到 settings.json 中，减少烦人的权限弹窗 | 新人配置环境、减少重复授权 |
| **claude-audit** | 审计 Claude Code 的使用情况，检查配置和权限设置 | 团队合规检查、排查配置问题 |
| **keybindings-help** | 自定义快捷键。查看、修改、绑定 Claude Code 键盘快捷键 | 设置常用操作的快捷键 |

### 5.2 Superpowers 系列（14 个）

obra 市场出品的系统性开发工作流套件，覆盖从需求→计划→实现→审查→验证全流程。

| Skill | 功能说明 | 什么时候用 |
|-------|---------|-----------|
| **using-superpowers** | Superpowers 总入口。首次使用会自动安装所有子 Skill。定义了完整的软件开发工作流 | 第一次使用 Superpowers 时必读 |
| **brainstorming** | 引导你进行结构化头脑风暴：明确问题→发散想法→收敛评估→行动计划。而不是漫无目的地聊 | 需求不明确、有多种方案可选时 |
| **writing-plans** | 根据需求编写分步骤实施计划。包含技术方案、文件清单、依赖关系、风险点 | 开始编码前制定路线图 |
| **executing-plans** | 按 writing-plans 生成的计划逐步执行，每完成一步打勾，遇到问题自动调整 | 按照计划有条不紊地开发 |
| **dispatching-parallel-agents** | 将任务拆解后分发给多个并行子智能体同时处理，最后汇总结果 | 大范围代码迁移、多文件重构 |
| **subagent-driven-development** | 把开发任务交给子智能体，你去 Review 结果。类似 PR 模式 | 你只想做架构决策不想写实现细节时 |
| **test-driven-development** | 强制先写测试后写代码的红-绿-重构循环 | 对质量要求高的核心模块 |
| **systematic-debugging** | 结构化的 5 步调试法：复现→提单→定位→修复→验证。告别凭感觉瞎猜 | 遇到难复现的 Bug、回归问题 |
| **requesting-code-review** | 生成代码审查请求，包含变更摘要、审查重点、上下文信息 | 团队协作时提请同事审查 |
| **receiving-code-review** | 指导如何处理 Review 意见：理解→分类→确认→修改→回复的闭环 | 收到 Code Review 反馈后 |
| **verification-before-completion** | 完成开发前强制运行验证清单：测试通过、类型检查、lint、构建、端到端验证 | 提交代码前最后一步 |
| **using-git-worktrees** | 教你如何在隔离的 Git Worktree 中开发，不影响当前工作区 | 同时维护多个分支、需要干净环境 |
| **finishing-a-development-branch** | 完成分支的标准流程：整理提交→同步主分支→清理 worktree→删除临时分支 | 一个功能开发完成后 |
| **writing-skills** | 教你如何编写自定义 Skill，包含模板、最佳实践、gotchas | 你想创建自己的 Skill 时 |

### 5.3 Example Skills（14 个）

Anthropic 提供的参考实现，适合作为编写自定义 Skills 的起点。

| Skill | 它能做什么 | 最适合谁 |
|-------|-----------|---------|
| **skill-creator** | 引导你一步步创建标准 Skill：定义名称/描述/触发条件→编写指令→测试→安装。这是学习 Skill 格式的最佳入门 | 第一次写 Skill 的人 |
| **mcp-builder** | 从零构建 MCP 服务器的完整教程和模板，包括工具定义、资源暴露、认证处理 | 需要为 Claude 写 MCP 服务的开发者 |
| **frontend-design** | 生成生产级前端代码，避免 AI 常见的"千篇一律"审美。有设计原则和组件规范 | 前端开发者做 UI 时 |
| **webapp-testing** | Playwright E2E 测试框架：页面对象模式、测试数据管理、CI 集成 | 需要自动化浏览器测试的团队 |
| **brand-guidelines** | 定义品牌色板、字体、Logo 使用规范，确保 AI 生成内容符合品牌一致性 | 设计师和品牌运营人员 |
| **doc-coauthoring** | 多轮交互式文档协作：大纲→初稿→反馈→修订，像和一个文档编辑一起工作 | 写技术文档、产品文档、白皮书 |
| **premium-ui** | 高级 UI 组件库，包含动画、交互模式、响应式适配 | 需要高质量 UI 组件的项目 |
| **algorithmic-art** | 使用数学/算法生成 SVG 艺术图形，描述需求自动生成代码 | 生成封面图、插画、动态背景 |
| **canvas-design** | 交互式画布应用设计思路和实现模式（拖拽、缩放、连线等） | 画布类产品开发（白板、流程图） |
| **internal-comms** | 自动聚合 Jira/GitHub/Slack 信息生成站会周报。支持自定义模板 | 团队管理者、Scrum Master |
| **slack-gif-creator** | 根据文字描述生成 GIF 并自动发送到 Slack channel | 活跃团队氛围、自动化通知 |
| **theme-factory** | 根据品牌色生成 VS Code / iTerm / Slack 等工具的主题文件 | 设计团队统一开发工具视觉 |
| **web-artifacts-builder** | 构建交互式 Web Artifacts（原型、演示、工具页面） | 快速做可交互原型 |
| **docx-mcp** | 通过 MCP 读写 DOCX 文档，支持模板填充、格式操作 | 需要程序化生成 Word 文档 |

### 5.4 社区精选 Skills（14 个）

从各大社区仓库精心筛选的实用 Skills。

| Skill | 功能说明 | 解决什么问题 |
|-------|---------|-------------|
| **adversarial-review** | 启动子智能体以"挑刺"视角审查代码，你 review 过的它还能找出遗漏的 bug。比你自己的 review 严格 10 倍 | 代码审查不够严格、总是放过低级错误 |
| **babysit-pr** | 自动监控 PR 状态：CI 失败自动重试、有冲突自动 rebase、review 完成自动 merge。PR 的全职保姆 | PR 堆积太多没时间跟进 |
| **token-discipline** | 7 个具体习惯帮你优化 Claude Code 上下文预算。比如"长参考放 Skill 不放 CLAUDE.md"、"定期 /doctor" | 上下文总是撑爆、频繁被截断 |
| **superteam** | 同时启动 7 个领域专家子智能体（架构、安全、性能、测试、可维护性、文档、用户体验）全面审计项目 | 大型项目需要多维度全面审查 |
| **signup-flow-driver** | 操作无头浏览器自动完成注册→邮箱验证→新用户引导的完整流程，截图 + 日志输出 | 新注册流程 QA、回归测试 |
| **funnel-query** | 帮你定义注册→激活→付费漏斗的每个步骤事件，生成 SQL/BI 查询 | 数据分析师做漏斗分析 |
| **new-migration** | 数据库迁移文件模板 + 所有边界情况清单（回滚、数据一致性、零停机）。避免线上事故 | 执行数据库迁移时 |
| **standup-post** | 自动从 Jira/GitHub/Slack 拉取你昨天的活动，按模板生成站会报告 | 每日站会前快速准备 |
| **log-correlator** | 给定一个请求 ID/用户 ID，自动从所有关联系统（后端、前端、数据库、CDN）拉取对应时间段的日志 | 排查线上问题时跨系统追日志 |
| **dependency-management** | 组织级依赖审批工作流：新依赖申请→安全检查→合规评估→记录 | 公司有依赖合规要求时 |
| **changelog** | 分析 git log 自动生成 Conventional Commits 格式的 CHANGELOG.md | 发布前更新 changelog |
| **pr-describe** | 分析 diff 自动生成 PR 描述：变更摘要、影响范围、测试说明、截图建议 | 提 PR 时懒得写描述 |
| **test-triage** | 分析测试失败原因自动分类（flaky / 回归 / 环境问题），支持批量处理 | 大量测试失败时迅速定位根因 |
| **billing-lib** | 记录内部计费库的所有边界情况、已知问题、使用模式。避免反复踩坑 | 使用内部计费 SDK 时 |

---

## 六、Cursor Rules & Skills

### 配置文件位置

```
.cursor/rules/          # 新版 Project Rules（推荐）
  ├── react.mdc         # 按 glob "src/**/*.tsx" 自动附加
  ├── api.mdc           # 按 glob "app/api/**/*.ts" 自动附加
  └── test.mdc          # 按 glob "**/*.test.ts" 自动附加
.cursor/skills/         # Skills 目录（Cursor 0.45+）
.cursorrules            # 旧版单个规则文件
```

### 社区资源

| 资源 | 链接 | 说明 |
|------|------|------|
| awesome-cursor-rules | [PatrickJS/awesome-cursor-rules](https://github.com/PatrickJS/awesome-cursor-rules) | Cursor 规则精选合集 |
| proagents | [Arlandaren/proagents](https://github.com/Arlandaren/proagents) | 794 个专家规则，支持 CLI 一键安装 |
| Cursor Directory | [cursor.directory](https://cursor.directory) | 官方规则市场 |

### 推荐 Cursor 规则

| 规则 | 功能说明 | glob 匹配 |
|------|---------|-----------|
| React 最佳实践 | 约束组件结构（函数式+interface Props）、禁止危险模式、强制 Hook 命名规范 | `src/**/*.tsx` |
| TypeScript 严格模式 | 禁止 any、强制泛型使用、约束类型导出方式 | `src/**/*.ts` |
| Tailwind CSS | 样式组织规范（原子类优先、响应式断点规则）、禁止内联 style | `src/**/*.{tsx,css}` |
| API 设计 | 路由命名、HTTP 方法选择、错误响应格式、输入验证 | `app/api/**/*.ts` |
| 测试规范 | 测试命名（should_xxx）、AAA 模式、Mock 范围控制 | `**/*.test.{ts,tsx}` |
| Git 工作流 | 提交信息格式（Conventional Commits）、分支命名规则 | `**/*` |

---

## 七、Windsurf Rules & Skills

### 配置文件位置

```
.windsurfrules          # 项目级主指令
.windsurf/rules/        # 分文件规则
.windsurf/skills/       # Skills 目录
.windsurf/agents/       # Agent 定义（除 Claude Code 外唯一原生支持）
```

### 社区资源

- [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills) — 原生支持 Windsurf 格式
- [WesleySmits/agent-skills](https://github.com/WesleySmits/agent-skills) — 43 个 Skills 兼容 Windsurf

---

## 八、GitHub Copilot Instructions

### 配置文件位置

```
.github/
├── copilot-instructions.md              # 主指令（全量注入）
└── instructions/
    ├── styling.instructions.md           # 代码风格
    ├── architecture.instructions.md      # 架构约束
    └── testing.instructions.md           # 测试规范
```

### 社区资源

- [awesome-copilot](https://github.com/slmingol/awesome-copilot) — custom agents、prompts、instructions 合集
- Copilot Extensions 市场 — MCP 服务器集成

> **重要：** Copilot 优先读取 `AGENTS.md`（如果项目中有），其次才是 `copilot-instructions.md`

### 推荐 Instructions

| 领域 | 典型内容 | 实际效果 |
|------|----------|----------|
| 代码风格 | 命名约定、缩进、注释规范、文件组织 | Copilot 补全的代码自动符合项目风格 |
| 架构约束 | 包依赖规则、分层架构、禁止的导入路径 | 防止架构腐化、循环依赖 |
| 测试要求 | 覆盖率目标、测试命名约定、Mock 策略 | 生成符合项目规范的测试用例 |
| 安全规范 | 输入验证、SQL 注入防护、XSS 预防 | 减少常见安全漏洞自动生成 |
| 数据库 | 迁移命名、模型定义、查询优化约定 | 保持数据库层代码的一致性 |

---

## 九、跨平台一站式方案

### AGENTS.md 开放标准

Linux Foundation / Agentic AI Foundation 推动，**60,000+ 项目已采用**，支持 **20+ 工具**。

支持平台：GitHub Copilot, Codex CLI, Cursor, Devin, Windsurf, Amp, Gemini CLI 等

```markdown
# AGENTS.md — Project Guide

## 技术栈
- 前端: React 18 + TypeScript + Tailwind
- 后端: Node.js + Express + Prisma
- 数据库: PostgreSQL
- 部署: Vercel + Docker

## 开发命令
- `npm run dev` — 启动开发服务器
- `npm run build` — 构建生产版本
- `npm test` — 运行测试
- `npm run lint` — 代码检查

## 代码规范
- ES module 语法（不使用 CommonJS）
- React 组件使用函数式 + Hooks，Props 用 interface 定义
- API 路由遵循 RESTful 设计，统一错误响应格式
```

### ai-rulez

> **一次定义，19+ 平台编译输出** —— 用一套规则源文件生成各平台原生配置，告别多份维护

```bash
pip install ai-rulez

# 目录结构（源文件）
.ai-rulez/
  ├── base.yaml        # 通用规则（所有平台通用）
  ├── react.yaml       # React 专属规则
  └── testing.yaml     # 测试规则

# 编译到各平台
ai-rulez compile --tool cursor     # → .cursor/rules/*.mdc
ai-rulez compile --tool claude     # → CLAUDE.md
ai-rulez compile --tool copilot    # → .github/copilot-instructions.md
ai-rulez compile --tool windsurf   # → .windsurfrules
```

- 33 个内置领域规则（开箱即用）
- 支持远程引用和组织级 profiles
- MCP 服务器集成

### skillrail

> **版本化 Skill 注册表 + CI 门禁** —— 规则像代码一样有版本、可审查、可回滚

```bash
skillrail check        # CI 中检查规则是否漂移（是否有人手工改了各平台配置）
skillrail status       # 查看所有 Skill 状态和版本
skillrail compile      # 从注册表编译到目标平台格式
```

### agent-rules-sync

> **一次编写，一键同步到所有平台**

```bash
npx agent-rules-sync sync     # 同步到所有已配置的平台
npx agent-rules-sync split    # 拆分模式（每平台独立文件，可分别定制）
```

- 支持：Claude, Cursor, Windsurf, Copilot, Gemini, Codex
- 自动摘要以适应各平台的大小限制

---

## 十、大型 Awesome 合集仓库

| 仓库 | ⭐ | 数量 | 核心功能 |
|------|----|------|----------|
| [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills) | **42k+** | **1,900+** | 全网最大合集，npm 一键安装 `npx antigravity-awesome-skills`，有搜索浏览 UI |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | **27k+** | **1,000+** | 官方团队出品（Anthropic/Google/Vercel/Stripe 等），质量最有保障 |
| [charlieviettq/awesome-agent-skill](https://github.com/charlieviettq/awesome-agent-skill) | — | 598 | 598 个可移植 SKILL.md，含 Asgard AI 平台全套（314 个） |
| [casualuser/awesome-agent-skills](https://github.com/casualuser/awesome-agent-skills) | — | 1,000+ | 人工精选，拒绝 AI 灌水，社区真实 Skills 为主 |
| [Arlandaren/proagents](https://github.com/Arlandaren/proagents) | — | 794 | 232 个智能体角色 + 521 个工作流清单，CLI 一键安装 |
| [WesleySmits/agent-skills](https://github.com/WesleySmits/agent-skills) | — | 43 | 43 个生产级 Skills，兼容 5 个平台，质量扎实 |
| [Kevinchamplin/claude-skills](https://github.com/Kevinchamplin/claude-skills) | — | 精选 | Claude Code 专属社区策展，适合参考学习 |
| [hoodini/ai-agents-skills](https://github.com/hoodini/ai-agents-skills) | — | 创意类 | 电影级落地页、视频制作、设计系统等创意 Skills |
| [scienceaix/agentskills](https://github.com/scienceaix/agentskills) | — | 论文+资源 | 学术视角：论文、框架工具、多智能体协作研究 |
| [JasonColapietro/suede-creator-skills](https://github.com/JasonColapietro/suede-creator-skills) | **166** | **67** | MIT 授权的 Claude Code 与 Codex Skills，覆盖多智能体编排、Codex 工作节点集群、代码审查、AI 评测、产品、设计和增长工作流 |
| [EgoAlpha/awesome-DeepAgent-skills](https://github.com/EgoAlpha/awesome-DeepAgent-skills) | — | 分类收录 | DeepAgent 框架，含 Skills vs MCP 优劣势对比 |
| [MuhammadUsmanGM/claude-code-best-practices](https://github.com/MuhammadUsmanGM/claude-code-best-practices) | — | 11 套模板 | 30+ 操作指南 + 项目模板 + 安全手册，落地首选 |
| [IsHexx/system-prompts-and-models-of-ai-tools-chinese](https://github.com/IsHexx/system-prompts-and-models-of-ai-tools-chinese) | — | 中文合集 | 全中文 System Prompt 翻译，适合国内开发者 |
| [Kshiteej006/system-prompts-and-models-of-ai-tools](https://github.com/Kshiteej006/system-prompts-and-models-of-ai-tools) | — | 7,000+ 行 | 30+ 工具的系统提示词原文大合集 |

---

## 十一、知名企业官方 Skills

各大公司官方团队出品的 Skills，质量最高、信息最权威。

| 来源 | 代表 Skills | 主要功能 |
|------|-------------|----------|
| **Anthropic** | claude-api, code-review, verify, deep-research | Claude Code 全套技能，详见[官方核心 Skills](#51-官方核心-skills15-个) |
| **Google Labs** | Gemini CLI Skills | Google Cloud 开发、Gemini API 调用、AI Studio 集成 |
| **Vercel** | Next.js, Vercel CLI, Edge Functions, Analytics | 前端全栈部署：从开发到上线的完整工作流 |
| **Stripe** | Stripe API, Webhooks, Checkout, Billing | 支付集成全流程：产品创建→支付→Webhook 处理→对账 |
| **Cloudflare** | Workers, Pages, D1, R2, KV, Queues | 边缘计算全家桶：无服务器函数→静态托管→数据库→存储 |
| **Netlify** | Deploy, Functions, Edge, Forms, Identity | JAMstack 部署：自动构建→分支部署→表单处理 |
| **Trail of Bits** | Slither, static analysis, audit checklists | 专业级安全审计：智能合约分析→代码静态分析→渗透测试 |
| **Sentry** | Error Tracking, Performance, Session Replay | 全栈监控：错误捕获→性能分析→用户回放 |
| **Expo** | React Native, EAS Build, Updates, Router | 移动端开发：RN 项目搭建→构建→热更新→路由 |
| **Hugging Face** | Transformers, Datasets, Inference, Hub | ML/AI 全流程：模型推理→数据集处理→Hub 发布 |
| **Figma** | Design API, Plugin SDK, Variables, REST API | 设计系统自动化：插件开发→变量同步→资源导出 |
| **Supabase** | Database, Auth, Realtime, Storage, Edge Functions | 后端即服务：数据库→认证→实时订阅→存储 |
| **Strapi** | Content API, Webhooks, Admin Panel, Media | 无头 CMS：内容建模→API 生成→媒体管理 |

> 以上 Skills 均收录于 [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

---

## 十二、按领域分类的 Skills

### 🎨 前端开发

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| frontend-design | Claude Code | 生成组件代码时遵循设计规范，避免 AI 常见的"千篇一律"审美 |
| web-artifacts-builder | Claude Code | 构建交互式 Web 原型/演示页面，支持实时预览 |
| premium-ui | Claude Code | 高级 UI 组件库：动画、过渡、交互模式，不依赖 UI 框架 |
| React 组件规范 | Cursor/Windsurf | 约束组件结构、Hook 命名、Props 类型定义 |
| Tailwind CSS | Cursor/Windsurf | 样式组织规范：原子类优先、断点规则、禁止内联 style |
| Expo Skills | 多平台 | React Native 移动端：项目初始化→EAS Build→OTA 更新 |

### 🏗️ 后端 / API

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| API 设计规范 | 通用 | REST/GraphQL 端点设计模式：路由命名、错误格式、版本策略 |
| new-migration | Claude Code | 生成数据库迁移文件，包含回滚脚本、边界情况检查清单 |
| dependency-management | Claude Code | 新依赖引入时的审批流程：安全扫描→合规检查→记录 |
| Stripe API Skills | 多平台 | 支付集成：商品创建→支付 intent→Webhook 对账 |
| Supabase Skills | 多平台 | 后端即服务：数据库设计→Row Level Security→实时订阅 |

### 🤖 AI / ML

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| claude-api | Claude Code | Claude/Anthropic SDK 完全参考：模型选择→参数调优→缓存策略 |
| deep-research | Claude Code | 联网搜索→多源抓取→交叉验证→生成带引用的研究报告 |
| Hugging Face Skills | 多平台 | Transformers 模型推理→数据集加载→Hub 发布→Inference API |
| algorithmic-art | Claude Code | 用数学算法生成 SVG 艺术图形，可导出为矢量图 |

### 📊 数据 / 分析

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| dataviz | Claude Code | 自动选图表类型→配色方案验证→生成美观的可视化图表 |
| funnel-query | Claude Code | 定义漏斗事件→生成 SQL/BI 查询→分析用户转化路径 |
| csv-analysis | 通用 | CSV 文件快速统计→异常检测→生成结构化分析报告 |
| log-correlator | Claude Code | 给定请求 ID，从后端/前端/数据库/CDN 日志中关联拉取完整链路 |

### 🔧 开发运维

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| code-review | Claude Code | 分析 diff 找出 bug、重复代码、性能问题，提供修改建议 |
| systematic-debugging | Claude Code | 5 步调试法：复现→提单→定位→修复→验证 |
| tdd | Claude Code | 强制红-绿-重构循环，先写测试再写实现 |
| using-git-worktrees | Claude Code | 在隔离的 Git Worktree 中开发，不干扰当前工作区 |
| babysit-pr | Claude Code | 自动监控 PR：CI 重试→冲突解决→合并 |
| git-workflow | 通用 | 分支策略→提交信息规范→合并约定→Release 流程 |

### 📝 内容 / 文档

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| brand-guidelines | Claude Code | 定义品牌色/字体/Logo 规范，确保 AI 输出符合品牌一致性 |
| doc-coauthoring | Claude Code | 多轮交互式文档写作：大纲→初稿→反馈→修订 |
| internal-comms | Claude Code | 自动聚合 Jira/GitHub/Slack 活动生成站会报告和周报 |
| changelog | 通用 | 分析 git log 生成 Conventional Commits 格式的 CHANGELOG |
| pr-describe | 通用 | 分析 diff 自动生成 PR 描述：变更摘要→影响范围→测试说明 |

### 🧪 测试 / 质量

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| verify | Claude Code | 运行你的应用并操作受影响的功能，观察实际行为验证改动的正确性 |
| simplify | Claude Code | 审查并自动应用代码简化：消除重复→提升可读性→优化性能 |
| webapp-testing | Claude Code | Playwright 端到端测试：页面对象模式→数据管理→CI 集成 |
| test-triage | Claude Code | 测试失败自动分类：flaky vs 回归 vs 环境问题 |
| Trail of Bits | 多平台 | 专业级安全审计：Slither 静态分析→OWASP 检查清单 |

### 🔒 安全

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| security-review | Claude Code | 全量安全检查：SQL 注入→XSS→CSRF→认证绕过→密钥泄露 |
| secret-blocking hooks | 通用 | 提交前自动扫描并阻止密钥、Token、密码等敏感信息被提交 |
| adversarial-review | Claude Code | 子智能体以攻击者视角审查代码，发现防御性编程遗漏 |

### 🎬 创意 / 多媒体

| Skill | 平台 | 它能做什么 |
|-------|------|-----------|
| theme-factory | Claude Code | 根据品牌色自动生成 VS Code / iTerm / Slack 主题文件 |
| canvas-design | Claude Code | 交互式画布 UI 模式：拖拽→缩放→连线→无限画布 |
| cinema landing pages | AI Agents Skills | 生成电影级视觉效果落地页：Parallax 滚动→动画→3D 效果 |
| video editing | AI Agents Skills | 视频制作工作流：脚本→分镜→剪辑→导出 |

---

## 十三、CLAUDE.md 模板（可直接用）

以下模板来自 [MuhammadUsmanGM/claude-code-best-practices](https://github.com/MuhammadUsmanGM/claude-code-best-practices) 的实践总结，可直接复制到项目中使用。

### React + TypeScript 项目

```markdown
# CLAUDE.md — React + TypeScript

## 技术栈
- 框架: React 18 + TypeScript
- 构建: Vite
- 样式: Tailwind CSS
- 测试: Vitest + React Testing Library
- 包管理: pnpm

## 构建命令
- `pnpm dev` — 启动开发服务器
- `pnpm build` — 生产构建
- `pnpm test` — 运行测试
- `pnpm lint` — ESLint

## 代码规范
- React 组件使用箭头函数 + `interface Props`
- 文件命名: `PascalCase`（组件）/ `camelCase`（工具函数）
- 状态管理使用 Zustand，避免 prop drilling
- API 调用使用 React Query (TanStack Query)
- 错误边界必须覆盖每个路由模块

## 目录结构
src/
  components/    # 通用组件
  features/      # 业务功能模块
  hooks/         # 自定义 Hooks
  lib/           # 工具函数
  pages/         # 页面组件
  types/         # TypeScript 类型定义
```

### Python + FastAPI 项目

```markdown
# CLAUDE.md — Python FastAPI

## 技术栈
- 框架: FastAPI + Pydantic v2
- ORM: SQLAlchemy 2.0 + Alembic
- 测试: pytest + httpx
- 包管理: uv / pip-tools

## 构建命令
- `uv run uvicorn app.main:app --reload` — 开发
- `pytest` — 运行测试
- `uv run alembic upgrade head` — 数据库迁移

## 代码规范
- 使用 `async def` 所有路由和数据库会话
- 请求/响应使用 Pydantic v2 model
- Repository 模式隔离数据库逻辑
- 异常使用自定义 HTTPException 子类
```

### Node.js + Express 项目

```markdown
# CLAUDE.md — Node.js Express

## 技术栈
- 运行时: Node.js 22
- 框架: Express + TypeScript
- 数据库: Prisma + PostgreSQL
- 测试: Vitest + Supertest
- 包管理: pnpm

## 构建命令
- `pnpm dev` — tsx watch
- `pnpm build` — tsc
- `pnpm test` — vitest

## 代码规范
- 中间件模式：auth → validation → controller → service → response
- 错误处理：全局 error handler middleware
- Controller 只做参数提取和响应，Service 做业务逻辑
- 所有 API 路由前缀 `/api/v1/`
```

### Go 项目

```markdown
# CLAUDE.md — Go

## 技术栈
- 语言: Go 1.23
- 框架: chi / gin
- 数据库: pgx + sqlc
- 测试: testing + testify
- 构建: Makefile

## 构建命令
- `make run` — 启动
- `make test` — 运行测试
- `make lint` — golangci-lint

## 代码规范
- 错误处理：永远不忽略 error 返回值
- 使用 `internal/` 包隔离实现细节
- Handler → Service → Repository 三层架构
- 配置通过环境变量注入
```

### Next.js 全栈项目

```markdown
# CLAUDE.md — Next.js

## 技术栈
- 框架: Next.js 15 (App Router)
- 语言: TypeScript
- 样式: Tailwind CSS + shadcn/ui
- 数据库: Prisma + PostgreSQL
- 部署: Vercel

## 构建命令
- `pnpm dev` — 本地开发
- `pnpm build` — 构建
- `pnpm test` — 测试
- `pnpm lint` — 代码检查

## 架构规范
- App Router: `app/` 目录下按路由分组
- Server Component 优先，Client Component 最小化
- API 路由: `app/api/**/route.ts`
- 数据获取在 Server Component 中直接执行
- 表单使用 Server Actions
```

---

## 十四、Agent Skills 最佳实践

### 14.1 Skill 编写的 6 条黄金法则

来自 Anthropic 官方团队（[Lessons from building Claude Code](https://claude.com/blog/lessons-from-building-claude-code-how-we-use-skills)）：

1. **不要写显而易见的内容** — Claude 已经会编码，你的 Skill 应提供它 **不知道** 的专有知识（边界情况、内部约定、历史原因）
2. **建立 Gotchas 板块** — 边界情况、已知问题、容易犯错的地方。这是 Skill 中价值最高的内容
3. **善用文件系统** — `references/` 放长篇文档、`scripts/` 放可执行脚本、`assets/` 放资源文件。用目录结构渐进揭示
4. **避免过度约束** — 足够具体让模型做对，但保留灵活性让模型能处理意外情况
5. **描述写给模型看** — `description` 字段说明**什么场景触发**这个 Skill（例如 "当用户要求部署到生产环境时"），而不是写给人类的摘要
6. **存储可执行脚本** — 把 Python/Bash/Node 脚本放在 `scripts/` 目录下，让 Claude 专注于组合调用而非从头编写

### 14.2 标准 Skill 文件结构

```
skills/<skill-name>/
├── SKILL.md            # 必需 — YAML frontmatter + 主指令
├── REFERENCE.md        # 可选 — 详细参考文档（SKILL.md 过长时拆分）
├── scripts/            # 可选 — 辅助脚本（Python/Bash/Node）
│   └── analyze.py
├── templates/          # 可选 — 输出模板
│   └── report-template.md
├── schemas/            # 可选 — JSON Schema（用于结构化输出）
│   └── output.schema.json
└── assets/             # 可选 — 图片、Logo 等资源文件
    └── logo.png
```

### 14.3 SKILL.md 前置元数据

```yaml
---
name: my-custom-skill
description: 当用户提到 X、Y、Z 关键词时触发此 Skill。描述给模型看，不是给人看
allowed-tools: ["Skill", "TextEditor", "Bash", "Glob"]
version: "1.2.0"
---
```

### 14.4 Skill 质量自检清单

| 检查项 | 合格 ✅ | 不合格 ❌ |
|--------|---------|-----------|
| **独有知识** | 传授了模型训练数据中没有的内部知识 | 重复通用编码规范 |
| **描述精准度** | "当用户说 'deploy' 且项目使用 Docker 部署时" | "部署相关" |
| **长度控制** | SKILL.md < 500 行，过长内容放附属文件 | 单文件上万行 |
| **可维护性** | 有版本号 + 更新日志 | 没有版本信息 |
| **有 Gotchas** | "注意：当 X 条件成立时此步骤会失败，因为 Y" | 只有常规操作步骤 |
| **脚本化** | 关键操作有现成脚本可复用 | 所有步骤让模型手写 |

### 14.5 目录位置

```bash
# 用户级（个人全局生效）
~/.claude/skills/<skill-name>/SKILL.md

# 项目级（团队共享，推荐 Git 管理）
your-project/.claude/skills/<skill-name>/SKILL.md
```

### 14.6 各平台对比总结

| 维度 | Claude Code | Cursor | Windsurf | Copilot |
|------|-------------|--------|----------|---------|
| 指令文件 | `CLAUDE.md` | `.cursorrules` / `.mdc` | `.windsurfrules` | `.github/copilot-instructions.md` |
| Skill 目录 | `.claude/skills/` | `.cursor/skills/` | `.windsurf/skills/` | `.github/instructions/` |
| 格式 | `SKILL.md` + 附属文件 | `.mdc` | `.md` | `.instructions.md` |
| 加载方式 | description 匹配触发 | glob 自动附加 | glob 自动附加 | 全量注入 |
| 子智能体 | ✅ `.claude/agents/` | ❌ | ✅ `.windsurf/agents/` | ❌ |
| YAML frontmatter | ✅ 支持 | ✅ 支持 | ✅ 支持 | ❌ 纯 Markdown |
| 跨平台 | 通过 AGENTS.md | 通过 AGENTS.md | 通过 AGENTS.md | 通过 AGENTS.md |

---

## 十五、常见陷阱 & 避坑指南

### 🕳️ 陷阱 1：CLAUDE.md 过于庞大

**表现：** CLAUDE.md 超过 500 行，每次加载就吃掉大量上下文预算，导致可用窗口缩短。

**正确做法：**
- CLAUDE.md 控制在 **200 行以内**，只放"每次会话都必须知道"的内容
- 长篇参考文档做成 Skill（按需加载，不用不占预算）
- 详细技术规范放进 `.claude/rules/` 目录（路径匹配触发）

### 🕳️ 陷阱 2：一个 Skill 试图包罗万象

**表现：** 一个 Skill 的描述写了 5 种不同场景，结果哪个场景都匹配不准。

**正确做法：**
- **一个 Skill 只做一件事**
- description 精准到关键词级别（"用户要求部署到生产环境"而非"部署相关"）
- 多个相关 Skill 通过名称前缀关联（`deploy-dev`, `deploy-staging`, `deploy-prod`）

### 🕳️ 陷阱 3：用错机制

**表现：** 部署流程放 CLAUDE.md 里 → 每次会话加载用不到的内容。频繁运行的任务每次都手写 → 浪费 token。

**正确做法：**
- 每周用 3 次以上 → **Skill**（按需加载，用完即走）
- 每次会话都知道 → **CLAUDE.md**（自动加载，始终可用）
- 复杂流程涉及多轮对话 → **Subagent**（独立上下文不污染主窗口）

### 🕳️ 陷阱 4：不验证就提交

**表现：** 写完代码直接提交，CI 红了才发现有问题。

**正确做法：**
- 养成提交前跑 `/verify` 的习惯
- 设置 PreToolUse hook 强制运行 lint + 测试
- 提交信息遵循 Conventional Commits

### 🕳️ 陷阱 5：Skills 版本不受控

**表现：** Skills 散落在 `~/.claude/skills/` 里，团队成员各用各的版本。

**正确做法：**
- Skills 和项目代码一起 Git 管理（`.claude/skills/` 下）
- 使用 skillrail 或 ai-rulez 做集中管理
- 有版本号和变更记录

### 🕳️ 陷阱 6：安装太多 Skills

**表现：** `~/.claude/skills/` 里装了几十个 Skills，光读元数据就消耗大量 token。

**正确做法：**
- 用户级只保留高频通用的 5-10 个
- 项目级放该项目专属的
- 定期跑 `/doctor` 检查预算状态

### 🕳️ 陷阱统计速查

| 陷阱 | 频率 | 严重度 | 一句话解决方案 |
|------|------|--------|---------------|
| CLAUDE.md 过大 | 🔴 常见 | 🔴 严重 | 200 行上限，长的放 Skill |
| Skill 职责过宽 | 🔴 常见 | 🟡 中等 | 一个 Skill 一件事 |
| 用错机制 | 🟡 偶尔 | 🟡 中等 | 参考[决策矩阵](#三决策矩阵该用哪种机制) |
| 不验证提交 | 🟡 偶尔 | 🔴 严重 | `/verify` + PreToolUse hook |
| 版本不受控 | 🟡 偶尔 | 🟡 中等 | Git 管理 `.claude/` |
| 安装太多 | 🟡 偶尔 | 🟡 中等 | 精简到 5-10 个 |

---

## 十六、快速入门推荐清单

### 🆕 新手 15 分钟入门

```bash
# 1. 创建 CLAUDE.md
cat > CLAUDE.md << 'EOF'
# CLAUDE.md — My Project

## 技术栈
[填写你的技术栈]

## 开发命令
- `npm run dev` — 启动开发
- `npm test` — 运行测试
EOF

# 2. 准备 Skills 目录
mkdir -p .claude/skills

# 3. 设置验证习惯（每次提交前跑一遍）
# claude /verify
```

### 🎯 必装精选手册

| 优先级 | Skill | 平台 | 为什么必装 | 第一次使用场景 |
|--------|-------|------|------------|---------------|
| ⭐⭐⭐ | **code-review** | Claude Code | 提交前自动审查 diff，拦截 80% 的低级错误 | 改完代码后说 "review this diff" |
| ⭐⭐⭐ | **verify** | Claude Code | 端到端验证比单元测试更全面，直接运行你的应用看效果 | 改完核心逻辑后跑 verify |
| ⭐⭐⭐ | **deep-research** | Claude Code | 多源搜索 + 交叉验证 + 引用报告，技术选型不再拍脑袋 | "帮我调研 React 19 vs Vue 4" |
| ⭐⭐⭐ | **skill-creator** | Claude Code | 学会写 Skill 是"元技能"——造了它，以后所有重复工作都能自动化 | "帮我创建一个 deploy skill" |
| ⭐⭐ | **mcp-builder** | Claude Code | MCP 是 AI 连接外部世界的桥梁，数据库/GitHub/API 全靠它 | "给我们的内部 API 写个 MCP 服务" |
| ⭐⭐ | **webapp-testing** | Claude Code | Playwright E2E 测试框架，比手动测试靠谱一万倍 | "给登录流程写个 E2E 测试" |
| ⭐⭐ | **systematic-debugging** | Claude Code | 结构化5步调试法，告别"改一行试试"的瞎猜模式 | "这个 Bug 我搞了两小时了" |
| ⭐⭐ | **security-review** | Claude Code | 上线前必过安全关，检查 SQL 注入/XSS/密钥泄露 | "帮我查一下这个 PR 有没有安全问题" |
| ⭐ | **dataviz** | Claude Code | 自动数据可视化 + 色板校验，图表好看且配色合理 | "帮我画一下这个月的数据趋势" |
| ⭐ | **AGENTS.md** | 全平台 | 一次编写到处运行，项目配置的"一次写对，到处生效" | 新项目初始化时 |

### 👨‍👩‍👧‍👦 团队实践建议

| 建议 | 具体做法 | ROI |
|------|----------|-----|
| 版本控制 | `.claude/` 目录纳入 Git 管理 | 🔴 高：团队统一、新人就绪 |
| 验证优先 | 花一周时间构建验证流程（verify Skill + CI hooks） | 🔴 高：提前拦 bug |
| Hooks 强制执行 | PreToolUse 让模型无法跳过 lint/secret-check | 🟡 中：减少人为疏忽 |
| 内部 Skills 市场 | 自然发现 → PR 评审 → 正式推广 三阶段 | 🟢 长期：知识沉淀 |
| Onboarding | 新人 `gh repo clone` 后 `.claude/` 自带全套规则 | 🟡 中：减少培训成本 |

### ⚡ Token 省钱 & 提效技巧

| 技巧 | 效果 | 做法 |
|------|------|------|
| 长参考放 Skill 不放 CLAUDE.md | 减少每次加载的 token | 按需触发，不用不加载 |
| 探索用 haiku | 降低 70%+ 成本 | `model: haiku` 做探索性分析 |
| Tool Search 替代全量 MCP 加载 | 减少约 85% MCP token | 先搜索再决定是否加载全部 |
| 定期 /doctor | 及早发现上下文超支 | 每周跑一次 `/doctor` |
| 清理不用的 Skills | 减少元数据加载 | `ls ~/.claude/skills/` 每季度审视 |

---

## 十七、参考链接汇总

### 📄 官方文档

| 标题 | 链接 | 一句话 |
|------|------|--------|
| Lessons from building Claude Code | [claude.com/blog](https://claude.com/blog/lessons-from-building-claude-code-how-we-use-skills) | Anthropic 官方 Skill 编写指南，必读 **⭐⭐⭐** |
| Steering Claude Code | [claude.com/de/blog](https://claude.com/de/blog/steering-claude-code-skills-hooks-rules-subagents-and-more) | 7 种定制机制对比 + 适用场景 |
| Power User Tips | [support.claude.com](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips) | Claude Code 团队亲授效率技巧 |

### ⭐ 精选仓库

| 仓库 | 链接 | 推荐理由 |
|------|------|----------|
| antigravity-awesome-skills | [GitHub](https://github.com/sickn33/antigravity-awesome-skills) | **42k ⭐** 1,900+ Skills，最大合集 |
| VoltAgent/awesome-agent-skills | [GitHub](https://github.com/VoltAgent/awesome-agent-skills) | **27k ⭐** 官方团队出品，质量最高 |
| claude-code-best-practices | [GitHub](https://github.com/MuhammadUsmanGM/claude-code-best-practices) | 11 套项目模板 + 安全手册 |
| WesleySmits/agent-skills | [GitHub](https://github.com/WesleySmits/agent-skills) | 43 个生产级 Skill，5 平台兼容 |
| Arlandaren/proagents | [GitHub](https://github.com/Arlandaren/proagents) | 794 个专家 Profile，CLI 安装 |
| awesome-cursor-rules | [GitHub](https://github.com/PatrickJS/awesome-cursor-rules) | Cursor 规则合集 |

### 🔧 跨平台管理工具

| 工具 | 链接 | 解决什么问题 |
|------|------|-------------|
| ai-rulez | [GitHub](https://github.com/Goldziher/ai-rulez) | 写一次规则，编译到 19+ 平台 |
| skillrail | [GitHub](https://github.com/gbouziden/skillrail) | 版本化 + CI 门禁 + 漂移检测 |
| agent-rules-sync | [NPM](https://www.npmjs.com/package/agent-rules-sync) | 跨平台规则一键同步 |

### 📝 深度分析

| 标题 | 链接 | 核心观点 |
|------|------|----------|
| 20 Skills Every Dev Should Install | [securityboulevard.com](https://securityboulevard.com/2026/06/20-claude-code-skills-every-developer-should-install-first/) | 6 维度评分推荐 |
| Skills vs MCP vs Plugins 完全指南 | [morphllm.com](https://www.morphllm.com/claude-code-skills-mcp-plugins) | 三种扩展机制对比 |
| 1400+ Skills 里的精华（中文） | [腾讯云](https://cloud.tencent.com.cn/developer/article/2671304) | 22% 的 Skill 质量不达标，5 问筛选法 |
| 四大定制机制指南（中文） | [阿里云](https://developer.aliyun.com/article/1745131) | CLAUDE.md vs Hook vs Skill vs Subagent |
| 兼容性矩阵 | [GitHub](https://github.com/codylindley/ai-harness-engineering-compatibility-matrix) | 各平台配置文件全映射 |

---

> **贡献指南**
> 欢迎通过 PR 添加新的 Skills 或更新已有信息。
> 提交信息请遵循 Conventional Commits 格式。

> **许可**
> CC0 1.0 Universal — 自由使用、分享、演绎
