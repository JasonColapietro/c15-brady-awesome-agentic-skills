# Awesome Agentic Skills 知识库

> 一份跨平台、跨工具的 AI Agent Skills 精选合集  
> 涵盖 Claude Code · Cursor · Windsurf · GitHub Copilot · Devin · Codex CLI · Gemini CLI · 等主流 AI 编程助手

---

## 📖 目录

- [一、生态概览](#一生态概览)
- [二、各平台配置文件对照](#二各平台配置文件对照)
- [三、Claude Code Skills](#三claude-code-skills)
  - [官方核心 Skills](#31-官方核心-skills)
  - [Superpowers 系列](#32-superpowers-系列)
  - [Example Skills](#33-example-skills)
  - [社区推荐 Skills](#34-社区推荐-skills)
- [四、Cursor Rules & Skills](#四cursor-rules--skills)
- [五、Windsurf Rules & Skills](#五windsurf-rules--skills)
- [六、GitHub Copilot Instructions](#六github-copilot-instructions)
- [七、跨平台一站式方案](#七跨平台一站式方案)
  - [AGENTS.md 开放标准](#71-agentsmd-开放标准)
  - [ai-rulez](#72-ai-rulez)
  - [skillrail](#73-skillrail)
  - [agent-rules-sync](#74-agent-rules-sync)
- [八、大型 Awesome 合集仓库](#八大型-awesome-合集仓库)
- [九、知名企业官方 Skills](#九知名企业官方-skills)
- [十、按领域分类的 Skills](#十按领域分类的-skills)
- [十一、Agent Skills 最佳实践](#十一agent-skills-最佳实践)
  - [Skill 编写原则](#111-skill-编写原则)
  - [Skill 文件结构](#112-skill-文件结构)
  - [目录结构](#113-目录结构)
  - [各平台对比总结](#114-各平台对比总结)
- [十二、快速入门推荐清单](#十二快速入门推荐清单)
- [十三、参考链接汇总](#十三参考链接汇总)

---

## 一、生态概览

| 平台 | 规则机制 | Skills 目录 | 加载方式 | 社区星数 |
|------|----------|------------|----------|----------|
| **Claude Code** | `CLAUDE.md` + `.claude/rules/` | `.claude/skills/*/SKILL.md` | 按需触发（description 匹配） | - |
| **Cursor** | `.cursorrules` / `.cursor/rules/*.mdc` | `.cursor/skills/` | 全局匹配 + Auto Attached | - |
| **Windsurf** | `.windsurfrules` / `.windsurf/rules/` | `.windsurf/skills/` | 按规则文件 glob 匹配 | - |
| **GitHub Copilot** | `.github/copilot-instructions.md` | `.github/instructions/*.instructions.md` | 会话注入 | - |
| **Codex CLI** | `CLAUDE.md` + rules | Skills 目录 | 按需加载 | - |
| **Gemini CLI** | `GEMINI.md` + rules | Skills 目录 | 按需加载 | - |
| **AGENTS.md** | `AGENTS.md`（Linux Foundation 标准） | 跨平台统一 | 60k+ 项目采用 | ⭐ |

---

## 二、各平台配置文件对照

| 配置文件 | 支持的平台 | 说明 |
|----------|-----------|------|
| `CLAUDE.md` | Claude Code, Codex CLI | 项目级指令，会话开始自动加载 |
| `.claude/rules/*.md` | Claude Code | 路径作用域规则，触及时加载 |
| `.claude/skills/*/SKILL.md` | Claude Code, Codex, Gemini CLI | 按 name/description 触发 |
| `.claude/agents/*.md` | Claude Code | 子智能体定义 |
| `.cursorrules` | Cursor（旧版） | 项目级指令 |
| `.cursor/rules/*.mdc` | Cursor（新版 Project Rules） | 基于 glob 自动附加 |
| `.cursor/skills/` | Cursor | Skills 目录 |
| `.windsurfrules` | Windsurf | 项目级指令 |
| `.windsurf/rules/*.md` | Windsurf | 规则文件 |
| `.windsurf/skills/` | Windsurf | Skills 目录 |
| `.github/copilot-instructions.md` | GitHub Copilot | 项目级指令 |
| `.github/instructions/*.instructions.md` | GitHub Copilot | 分领域指令 |
| `AGENTS.md` | Copilot, Codex, Cursor, Devin 等 20+ 工具 | Linux Foundation 开放标准 |
| `GEMINI.md` | Gemini CLI | Google 的 CLAUDE.md 等价物 |

---

## 三、Claude Code Skills

### 3.1 官方核心 Skills

Anthropic 官方团队出品的 Skills，质量最高、维护最活跃。

| Skill | 描述 | 用途 |
|-------|------|------|
| **claude-api** | Claude API / Anthropic SDK 参考 | 模型 ID、定价、参数、流式、工具调用、MCP、缓存 |
| **claude-audit** | Claude Code 审计 | 检查使用情况和配置 |
| **code-review** | Code Review | 审查当前 diff 的 bug/可重用性/效率问题 |
| **deep-research** | 深度研究 | 多源搜索、对抗验证、合成引用报告 |
| **verify** | 端到端验证 | 执行受影响流程并观察行为，确保代码变更正确 |
| **simplify** | 代码简化 | 审查并自动应用可重用/简化/效率改进 |
| **run** | 启动并驱动应用 | 查看变更在真实应用中的效果 |
| **init** | 项目初始化 | 初始化新项目 |
| **review** | 代码审查 | 审查变更 |
| **security-review** | 安全审查 | 安全漏洞审查 |
| **update-config** | 配置更新 | 修改 settings.json 等配置 |
| **keybindings-help** | 快捷键自定义 | 修改键盘绑定 |
| **fewer-permission-prompts** | 权限优化 | 扫描常用命令并加入白名单减少权限提示 |
| **loop** | 循环任务 | 定时重复执行任务 |
| **dataviz** | 数据可视化 | 创建图表、图形、仪表盘，提供色板校验工具 |

### 3.2 Superpowers 系列

obra 市场出品的系统性开发工作流 Skills，提供完整的软件开发纪律。

| Skill | 描述 | 级别 |
|-------|------|------|
| **using-superpowers** | Superpowers 入口 | 流程 |
| **brainstorming** | 结构化头脑风暴 | 流程 |
| **dispatching-parallel-agents** | 并行智能体调度 | 流程 |
| **writing-plans** | 编写实施计划 | 流程 |
| **executing-plans** | 按照计划执行 | 流程 |
| **subagent-driven-development** | 子智能体驱动开发 | 流程 |
| **test-driven-development** | 测试驱动开发 | 流程 |
| **requesting-code-review** | 请求代码审查 | 流程 |
| **receiving-code-review** | 接收代码审查 | 流程 |
| **verification-before-completion** | 完成前验证 | 流程 |
| **using-git-worktrees** | Git Worktree 使用 | 流程 |
| **finishing-a-development-branch** | 完成开发分支 | 流程 |
| **systematic-debugging** | 系统性调试 | 流程 |
| **writing-skills** | 编写 Skills | 流程 |

### 3.3 Example Skills

Anthropic 官方提供的示例 Skills，是学习 Skill 编写的最佳参考。

| Skill | 描述 |
|-------|------|
| **algorithmic-art** | 算法艺术生成 |
| **brand-guidelines** | 品牌规范管理 |
| **canvas-design** | 画布设计 |
| **doc-coauthoring** | 文档协作编写 |
| **frontend-design** | 前端设计（避免通用 AI 审美） |
| **internal-comms** | 内部沟通自动化 |
| **mcp-builder** | 构建 MCP 服务器 |
| **skill-creator** | 编写新 Skills 的标准方法 |
| **slack-gif-creator** | Slack GIF 创建 |
| **theme-factory** | 主题工厂 |
| **web-artifacts-builder** | Web Artifacts 构建 |
| **webapp-testing** | Playwright UI 测试 |
| **premium-ui** | 高级 UI 组件 |
| **docx-mcp** | DOCX 文档处理 |

### 3.4 社区推荐 Skills

| Skill | 来源 | 描述 |
|-------|------|------|
| **token-discipline** | Kevinchamplin/claude-skills | 7 个习惯优化 Claude Code 上下文预算 |
| **superteam** | Kevinchamplin/claude-skills | 同时启动 7 个领域专家智能体进行项目全面审计 |
| **review** | Kevinchamplin/claude-skills | 部署前安全与质量审查 |
| **adversarial-review** | Anthropic 内部实践 | 启动"新视角"子智能体批判并修复代码 |
| **billing-lib** | Anthropic 内部实践 | 内部计费库边界情况参考 |
| **signup-flow-driver** | Anthropic 内部实践 | 无头浏览器注册→邮件验证→入门流程自动化 |
| **funnel-query** | Anthropic 内部实践 | 注册→激活→付费漏斗事件分析 |
| **standup-post** | Anthropic 内部实践 | 聚合工单、GitHub 活动、Slack 生成站会报告 |
| **new-migration** | Anthropic 内部实践 | 数据库迁移文件模板 + 常见陷阱 |
| **babysit-pr** | Anthropic 内部实践 | 监控 PR、重试失败 CI、解决冲突 |
| **log-correlator** | Anthropic 内部实践 | 给定请求 ID 从所有系统拉取对应日志 |
| **dependency-management** | Anthropic 内部实践 | 组织级依赖审批工作流 |
| **changelog** | claude-code-best-practices | 自动生成 CHANGELOG |
| **pr-describe** | claude-code-best-practices | 自动生成 PR 描述 |
| **test-triage** | claude-code-best-practices | 测试分类与管理 |

---

## 四、Cursor Rules & Skills

Cursor 使用 `.cursor/rules/*.mdc` 作为规则文件，支持基于 glob 的自动附加。

**配置文件位置：**
- 旧版：`./cursorrules`（项目根目录）
- 新版：`.cursor/rules/*.mdc`（支持 YAML 前置元数据 + 内容）
- Skills：`.cursor/skills/`

**规则文件示例（.mdc）：**

```yaml
---
description: React 组件编写规范
globs: src/components/**/*.tsx
---
```

**社区资源：**
- [awesome-cursor-rules](https://github.com) — Cursor 规则合集
- proagents 提供 794 个 Cursor 规则（232 个智能体角色 + 521 个工作流清单）

**推荐 Cursor Skills：**
| 规则 | 描述 |
|------|------|
| React/Next.js 最佳实践 | 组件结构、Hook 规范、性能优化 |
| TypeScript 严格模式 | TS 配置、类型安全规则 |
| Tailwind CSS 规范 | 样式组织、响应式设计规则 |
| API 设计规范 | REST/GraphQL 端点设计 |
| 测试规范 | Vitest/Playwright 测试规则 |
| Git 工作流 | 提交信息、分支策略 |

---

## 五、Windsurf Rules & Skills

Windsurf 使用 `.windsurfrules` 和 `.windsurf/rules/*.md`。

**配置文件位置：**
- `./windsurfrules` — 项目级指令
- `.windsurf/rules/*.md` — 分文件规则
- `.windsurf/skills/` — Skills 目录
- `.windsurf/agents/*.md` — Agent 定义

**社区资源：**
- [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills) 原生支持 Windsurf
- WesleySmits/agent-skills 43 个 Skills 支持 Windsurf

---

## 六、GitHub Copilot Instructions

GitHub Copilot 使用 `.github/copilot-instructions.md` 或 `.github/instructions/*.instructions.md`。

**配置文件位置：**
- `.github/copilot-instructions.md` — 主指令
- `.github/instructions/*.instructions.md` — 分领域指令

**社区资源：**
- [awesome-copilot](https://github.com/slmingol/awesome-copilot) — 社区贡献的 custom agents、prompts、instructions
- Copilot 的 Extensions 市场提供 MCP 集成

**推荐 Instructions：**
| 领域 | 描述 |
|------|------|
| 代码风格 | 项目特定的代码格式和命名约定 |
| 架构约束 | 包依赖规则、分层架构要求 |
| 测试要求 | 覆盖率目标、测试命名、mock 策略 |
| 安全规范 | 输入验证、认证、授权模式 |
| 数据库模式 | 迁移命名、模型定义约定 |

---

## 七、跨平台一站式方案

### 7.1 AGENTS.md 开放标准

Linux Foundation / Agentic AI Foundation 推动的开放标准，已有 **60,000+ 项目**采用，支持 **20+ 工具**。

**支持的平台：** GitHub Copilot, Codex CLI, Cursor, Devin Desktop, Windsurf, Amp, Gemini CLI 等

**格式示例（AGENTS.md）：**

```markdown
# AGENTS.md — Project Guide

## 技术栈
- 前端: React 18 + TypeScript
- 后端: Node.js + Express
- 数据库: PostgreSQL

## 构建命令
- `npm run build` — 构建生产版本
- `npm test` — 运行测试

## 代码规范
- 使用 ES module 语法
- React 组件使用函数式 + Hooks
- API 路由遵循 RESTful 设计
```

### 7.2 ai-rulez

> 一次定义，到处编译 — 支持 **19+ 工具**原生配置

- 仓库：[Goldziher/ai-rulez](https://github.com/Goldziher/ai-rulez)
- 安装：`pip install ai-rulez`
- 33 个内置领域规则
- 支持远程引用、配置文件（profiles）、MCP 服务器

**工作流：**
```
.ai-rulez/          # 规则源文件（一次编写）
  ├── base.yaml
  ├── react.yaml
  └── testing.yaml

# 编译到各平台
ai-rulez compile --tool cursor
ai-rulez compile --tool claude
ai-rulez compile --tool copilot
```

### 7.3 skillrail

> 版本化的 Skill 注册表，编译到 Claude、Cursor、Copilot、Windsurf

- 仓库：[gbouziden/skillrail](https://github.com/gbouziden/skillrail)
- CI 门禁：`skillrail check`
- 漂移检测：检测规则是否过时
- 按 Skill 维度定位目标平台

### 7.4 agent-rules-sync

> 跨平台规则同步工具

- NPM: [agent-rules-sync](https://www.npmjs.com/package/agent-rules-sync)
- 支持：Claude, Cursor, Windsurf, Copilot, Gemini, Codex
- 功能：单文件/拆分模式、自动摘要（适应大小限制）

---

## 八、大型 Awesome 合集仓库

| 仓库 | ⭐ Stars | Skills 数量 | 特色 |
|------|---------|-------------|------|
| [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills) | **42k+** | **1,900+** | 最大的合集；提供 npm CLI 安装 |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | **27k+** | **1,000+** | 官方团队 Skills（Anthropic、Google、Vercel 等） |
| [charlieviettq/awesome-agent-skill](https://github.com/charlieviettq/awesome-agent-skill) | — | 598 | 598 个可移植 SKILL.md；含 Asgard AI 平台包 |
| [casualuser/awesome-agent-skills](https://github.com/casualuser/awesome-agent-skills) | — | 1,000+ | 人工精选，社区真实 Skills |
| [Arlandaren/proagents](https://github.com/Arlandaren/proagents) | — | 794 | 232 个智能体角色 + 521 个工作流清单 |
| [WesleySmits/agent-skills](https://github.com/WesleySmits/agent-skills) | — | 43 | 43 个生产级 Skills，5 个平台兼容 |
| [Kevinchamplin/claude-skills](https://github.com/Kevinchamplin/claude-skills) | — | 精选 | 社区策展的 Claude Code Skills |
| [hoodini/ai-agents-skills](https://github.com/hoodini/ai-agents-skills) | — | 创意类 | 创意导向 Skills（视频、设计系统） |
| [scienceaix/agentskills](https://github.com/scienceaix/agentskills) | — | 论文+资源 | 学术论文、工具、框架合集 |
| [EgoAlpha/awesome-DeepAgent-skills](https://github.com/EgoAlpha/awesome-DeepAgent-skills) | — | 分类收录 | DeepAgent 框架；Skills vs MCP 对比 |
| [MuhammadUsmanGM/claude-code-best-practices](https://github.com/MuhammadUsmanGM/claude-code-best-practices) | — | 11 套模板 | 30+ 指南、项目模板、安全手册 |
| [IsHexx/system-prompts-and-models-of-ai-tools-chinese](https://github.com/IsHexx/system-prompts-and-models-of-ai-tools-chinese) | — | 中文合集 | 全中文，适合国内开发者 |
| [Kshiteej006/system-prompts-and-models-of-ai-tools](https://github.com/Kshiteej006/system-prompts-and-models-of-ai-tools) | — | 7,000+ 行 | 30+ 工具的 System Prompt 大合集 |

---

## 九、知名企业官方 Skills

各大公司官方出品的高质量 Skills：

| 来源 | Skills | 说明 |
|------|--------|------|
| **Anthropic** | claude-api, code-review, verify, deep-research 等 | Claude Code 核心 + Example Skills |
| **Google Labs** | Gemini CLI Skills | Gemini Code Assist 相关 |
| **Vercel** | Next.js, Vercel CLI Skills | Vercel 平台最佳实践 |
| **Stripe** | Stripe API, Webhooks Skills | Stripe 支付集成 |
| **Cloudflare** | Workers, Pages, D1 Skills | Cloudflare 生态 |
| **Netlify** | Deploy, Functions, Edge Skills | Netlify 平台 |
| **Trail of Bits** | Security Review Skills | 安全审计专用 |
| **Sentry** | Error Tracking, Performance Skills | Sentry 错误监控 |
| **Expo** | React Native, EAS Build Skills | 移动端开发 |
| **Hugging Face** | Transformers, Datasets Skills | ML/AI 开发 |
| **Figma** | Design API, Plugin Skills | 设计系统集成 |

> 以上企业 Skills 均收录于 [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

---

## 十、按领域分类的 Skills

### 🎨 前端开发

| Skill | 平台 | 描述 |
|-------|------|------|
| frontend-design | Claude Code | 生产级前端设计（避免通用 AI 审美） |
| React 组件规范 | Cursor/Windsurf | 组件结构、性能优化 |
| Tailwind CSS 规则 | Cursor/Windsurf | 样式组织和设计系统 |
| webapp-testing | Claude Code | Playwright UI 测试 |
| premium-ui | Claude Code | 高级 UI 组件开发 |
| web-artifacts-builder | Claude Code | Web Artifacts 构建 |

### 🏗️ 后端开发

| Skill | 平台 | 描述 |
|-------|------|------|
| API 设计规范 | 通用 | REST/GraphQL 端点设计 |
| 数据库迁移模板 | Claude Code | 迁移文件模板 + 常见陷阱 |
| 依赖管理 | Claude Code | 组织级依赖审批流程 |
| 安全审查 | 多平台 | OWASP 最佳实践 |

### 🤖 AI/ML 开发

| Skill | 平台 | 描述 |
|-------|------|------|
| claude-api | Claude Code | Claude API 参考 |
| algorithmic-art | Claude Code | 算法艺术生成 |
| Hugging Face Skills | 多平台 | Transformers、Datasets |

### 📊 数据分析

| Skill | 平台 | 描述 |
|-------|------|------|
| deep-research | Claude Code | 多源深度研究 |
| funnel-query | Claude Code | 业务漏斗分析 |
| csv-analysis | 通用 | CSV 统计分析 |
| dataviz | Claude Code | 数据可视化（带色板校验） |

### 🔧 开发运维

| Skill | 平台 | 描述 |
|-------|------|------|
| code-review | Claude Code | 代码审查（diff 分析） |
| test-driven-development | Claude Code | TDD 工作流 |
| systematic-debugging | Claude Code | 结构化调试 |
| using-git-worktrees | Claude Code | Git Worktree 隔离开发 |
| babysit-pr | Claude Code | PR 监控 + CI 重试 |
| git-workflow | 通用 | Git 约定和分支策略 |

### 📝 内容创作

| Skill | 平台 | 描述 |
|-------|------|------|
| brand-guidelines | Claude Code | 品牌规范 |
| doc-coauthoring | Claude Code | 文档协作 |
| internal-comms | Claude Code | 内部沟通自动化 |
| slack-gif-creator | Claude Code | Slack GIF 创建 |
| SEO 内容简报 | 通用 | 关键词聚类、意图分析 |

### 🧪 测试与质量

| Skill | 平台 | 描述 |
|-------|------|------|
| verify | Claude Code | 端到端行为验证 |
| simplifiy | Claude Code | 代码简化与重构 |
| test-triage | Claude Code | 测试分类管理 |
| webapp-testing | Claude Code | Playwright 端到端测试 |

### 🔒 安全

| Skill | 平台 | 描述 |
|-------|------|------|
| security-review | Claude Code | 安全漏洞审查 |
| Trail of Bits Skills | 多平台 | 专业安全审计 |
| secret-blocking hooks | 通用 | 防止密钥泄露 |

### 🎬 创意 & 多媒体

| Skill | 平台 | 描述 |
|-------|------|------|
| theme-factory | Claude Code | 主题工厂 |
| canvas-design | Claude Code | 画布设计 |
| cinematic landing pages | AI Agents Skills | 电影感落地页 |
| video editing | AI Agents Skills | 视频编辑工作流 |

---

## 十一、Agent Skills 最佳实践

### 11.1 Skill 编写原则

**Anthropic 官方团队总结的黄金原则：**

1. **不要写显而易见的内容** — Claude 已经知道如何编码，你的 Skill 应提供它不知道的特有知识
2. **建立 Gotchas 板块** — 这是 Skill 中最有价值的内容（边界情况、常见陷阱）
3. **善用文件系统** — 通过文件夹分层渐进显示（`references/`, `scripts/`, `assets/`）
4. **避免过度约束** — 足够具体但保留灵活性
5. **描述写给模型看** — 描述字段应该说明*何时触发*此 Skill，而非写给人类
6. **存储脚本** — 给 Claude 代码文件让它专注于组合而非重建

**技能质量过滤（腾讯云社区建议）：**
1. ❓ 是否传授了 Claude 不知道的知识？
2. ❓ 描述是否足够精确？
3. ❓ SKILL.md 是否在 500 行以内？
4. ❓ 最近是否维护更新？
5. ❓ 每周使用 3 次以上？

### 11.2 Skill 文件结构

**最小结构：**
```
skills/<skill-name>/
└── SKILL.md           # 必需 — YAML 前置元数据 + 指令
```

**完整结构：**
```
skills/<skill-name>/
├── SKILL.md            # 必需 — 前置元数据 + 主指令
├── REFERENCE.md        # 可选 — 详细参考文档
├── scripts/            # 可选 — Python、Bash、Node 脚本
│   └── analyze.py
├── templates/          # 可选 — 可复用模板
│   └── brief_template.md
├── schemas/            # 可选 — JSON Schema
│   └── output.schema.json
├── references/         # 可选 — 文档/资源
│   └── api-docs.md
└── assets/             # 可选 — 图片、Logo
    └── logo.png
```

**SKILL.md 前置元数据示例：**

```yaml
---
name: my-skill
description: 什么场景触发此 Skill（写给模型看，不是给人看）
allowed-tools: ["Skill", "TextEditor", "Bash"]
version: "1.2.0"
---
```

### 11.3 目录结构

**用户级（跨项目）：**
```
~/.claude/
├── skills/
│   ├── code-review/
│   │   └── SKILL.md
│   └── git-workflow/
│       └── SKILL.md
└── agents/
    └── ...
```

**项目级（团队共享，建议 Git 管理）：**
```
your-project/
├── CLAUDE.md
└── .claude/
    ├── settings.json
    ├── rules/
    │   └── frontend-rules.md
    └── skills/
        └── deploy-flow/
            └── SKILL.md
```

### 11.4 各平台对比总结

| 维度 | Claude Code | Cursor | Windsurf | Copilot |
|------|-------------|--------|----------|---------|
| 指令格式 | `CLAUDE.md` | `.cursorrules` / `.mdc` | `.windsurfrules` | `.github/copilot-instructions.md` |
| Skills 目录 | `.claude/skills/` | `.cursor/skills/` | `.windsurf/skills/` | `.github/instructions/` |
| Skill 格式 | `SKILL.md` + 可选文件 | `.mdc` 规则文件 | `.md` 规则文件 | `.instructions.md` |
| 加载机制 | 按 description 匹配触发 | glob 自动附加 | glob 自动附加 | 全量注入 |
| 子智能体 | ✅ `.claude/agents/` | ❌ 原生不支持 | ✅ `.windsurf/agents/` | ❌ 原生不支持 |
| 前置元数据 | ✅ YAML frontmatter | ✅ YAML frontmatter | ✅ YAML frontmatter | ❌ 纯 Markdown |
| 跨平台兼容 | 通过 AGENTS.md | 通过 AGENTS.md | 通过 AGENTS.md | 通过 AGENTS.md |

---

## 十二、快速入门推荐清单

### 🆕 新手入门

1. **写一个 CLAUDE.md** — 从 [claude-code-best-practices](https://github.com/MuhammadUsmanGM/claude-code-best-practices) 的模板开始
2. **安装 3-5 个核心 Skills**：
   - `skill-creator` — 学会创建 Skills
   - `code-review` — 代码审查
   - `deep-research` — 深度研究
   - `dataviz` — 数据可视化
   - `verify` — 端到端验证
3. **设置验证机制** — `/verify` 或 `/simplify` 自动化质量检查
4. **使用 AGENTS.md** — 一次编写，多平台兼容

### 👨‍👩‍👧‍👦 团队建议

- 将 Skills 纳入 Git 版本管理（放在 `.claude/skills/` 下）
- 创建验证 Skill — 花一周时间构建验证流程的团队 ROI 最高
- 使用 PreToolUse hooks 强制执行规范
- 建立内部 Skills 市场：自然发现 → PR 评审推广

### ⚡ 省钱技巧

- 长参考材料放 Skills 而非 CLAUDE.md（按需加载）
- 探索性任务使用 `model: haiku` + `isolation: fork`
- 使用 Tool Search 降低 MCP token 开销约 85%
- 定期运行 `/doctor` 检查 Skill 上下文预算状态

### 🎯 精选手册（必装清单）

| 优先级 | Skill | 平台 | 理由 |
|--------|-------|------|------|
| ⭐⭐⭐ | code-review | Claude Code | 每次提交都需审查 |
| ⭐⭐⭐ | verify | Claude Code | 验证比测试更重要 |
| ⭐⭐⭐ | deep-research | Claude Code | 多源深度研究利器 |
| ⭐⭐⭐ | skill-creator | Claude Code | 编写自定义 Skills 的起点 |
| ⭐⭐ | mcp-builder | Claude Code | 构建 MCP 服务器 |
| ⭐⭐ | webapp-testing | Claude Code | E2E 测试 |
| ⭐⭐ | systematic-debugging | Claude Code | 结构化调试 |
| ⭐⭐ | security-review | Claude Code | 安全审计 |
| ⭐ | dataviz | Claude Code | 数据可视化 |
| ⭐ | AGENTS.md | 全平台 | 跨平台兼容标准 |

---

## 十三、参考链接汇总

### 📄 官方文档

- [Anthropic — Lessons from building Claude Code: How we use skills](https://claude.com/blog/lessons-from-building-claude-code-how-we-use-skills)
- [Anthropic — Steering Claude Code: skills, hooks, subagents and more](https://claude.com/de/blog/steering-claude-code-skills-hooks-rules-subagents-and-more)
- [Claude Code Power User Tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### ⭐ 大型合集

- [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills) — 1,900+ Skills ⭐42k
- [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) — 1,000+ Skills ⭐27k
- [claude-code-best-practices](https://github.com/MuhammadUsmanGM/claude-code-best-practices) — 最佳实践手册
- [Kevinchamplin/claude-skills](https://github.com/Kevinchamplin/claude-skills) — 社区策展
- [WesleySmits/agent-skills](https://github.com/WesleySmits/agent-skills) — 43 个生产级 Skills
- [Arlandaren/proagents](https://github.com/Arlandaren/proagents) — 794 个专家 Prompt
- [hoodini/ai-agents-skills](https://github.com/hoodini/ai-agents-skills) — 创意类 Skills
- [IsHexx/system-prompts-and-models-of-ai-tools-chinese](https://github.com/IsHexx/system-prompts-and-models-of-ai-tools-chinese) — 中文合集
- [Kshiteej006/system-prompts-and-models-of-ai-tools](https://github.com/Kshiteej006/system-prompts-and-models-of-ai-tools) — System Prompt 大合集

### 🔧 跨平台工具

- [ai-rulez](https://github.com/Goldziher/ai-rulez) — 一次编写，19+ 平台编译
- [skillrail](https://github.com/gbouziden/skillrail) — 版本化 Skill 注册表
- [agent-rules-sync](https://www.npmjs.com/package/agent-rules-sync) — 跨平台规则同步
- [skill-rules](https://www.npmjs.com/package/skill-rules) — 环境分阶段 Skill 管理

### 📝 分析评测

- [20 Claude Code Skills Every Developer Should Install First](https://securityboulevard.com/2026/06/20-claude-code-skills-every-developer-should-install-first/)
- [Claude Code Skills vs MCP vs Plugins: Complete Guide 2026](https://www.morphllm.com/claude-code-skills-mcp-plugins)
- [Claude Code 1400+ 个 Skills 里的精华（腾讯云）](https://cloud.tencent.com.cn/developer/article/2671304)
- [四大定制机制完全指南（阿里云）](https://developer.aliyun.com/article/1745131)
- [AI Harness Engineering Compatibility Matrix](https://github.com/codylindley/ai-harness-engineering-compatibility-matrix)
- [AI Agent 配置文件到底该怎么写（腾讯云）](https://cloud.tencent.cn/developer/article/2686951)

---

> **贡献指南**
> 欢迎通过 PR 添加新的 Skills 或更新已有信息。  
> 本仓库使用 `gh` CLI 管理，提交信息请遵循 Conventional Commits 格式。

> **许可**
> CC0 1.0 Universal — 自由使用、分享、演绎
