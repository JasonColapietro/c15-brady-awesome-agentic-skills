<h1 align="center">Awesome Agentic Skills</h1>

<p align="center">
  <b>🚀 跨平台 AI Agent Skills 精选知识库</b><br>
  涵盖 Claude Code · Cursor · Windsurf · GitHub Copilot · Codex CLI · Gemini CLI · 等主流 AI 编程助手
</p>

<p align="center">
  <a href="https://github.com/bradyliuY/awesome-agentic-skills">
    <img src="https://img.shields.io/badge/skills-100%2B-blue" alt="Skills">
  </a>
  <a href="https://github.com/bradyliuY/awesome-agentic-skills">
    <img src="https://img.shields.io/badge/platforms-7%2B-green" alt="Platforms">
  </a>
  <a href="https://github.com/bradyliuY/awesome-agentic-skills">
    <img src="https://img.shields.io/badge/license-CC0-orange" alt="License">
  </a>
</p>

---

## 📋 简介

**Awesome Agentic Skills** 是一个精选的跨平台 AI Agent Skills 知识库。

无论你用 **Claude Code**、**Cursor**、**Windsurf**、**GitHub Copilot** 还是其他 AI 编程工具，这里都有你需要的最佳实践、现成模板和实用资源。

> 💡 **Skill 是什么？** Skill 是一份结构化的指令文件，告诉 AI 助手如何执行特定任务——比如代码审查、部署流程、数据分析。每个 Skill 包含 YAML 元数据和 Markdown 指令，按需加载。

---

## 🚀 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/bradyliuY/awesome-agentic-skills.git

# 2. 查看完整知识库
# 打开 awesome-agentic-skills.md

# 3. 创建你的第一个 Skill
mkdir -p .claude/skills/my-skill
```

[📖 查看完整知识库 →](awesome-agentic-skills.md)

---

## 📚 内容结构

```
awesome-agentic-skills/
├── README.md                         # 本文件
├── awesome-agentic-skills.md         # 📖 完整知识库（核心内容）
│
├── 生态概览 & 平台对照 ────────── 一 ~ 二章
├── 决策矩阵 & 快速上手 ────────── 三 ~ 四章
├── Skills 大全（Claude Code） ──── 第五章
├── Cursor / Windsurf / Copilot ──── 六 ~ 八章
├── 跨平台方案 & 合集仓库 ──────── 九 ~ 十章
├── 企业官方 Skills ────────────── 第十一章
├── 按领域分类 ────────────────── 第十二章
├── CLAUDE.md 模板 ────────────── 第十三章
├── 最佳实践 & 避坑指南 ──────── 十四 ~ 十五章
└── 推荐清单 & 参考链接 ──────── 十六 ~ 十七章
```

---

## 🎯 核心亮点

### ✅ 覆盖 7+ 主流平台

| 平台 | 配置机制 | Skills 支持 |
|------|----------|-------------|
| **Claude Code** | `CLAUDE.md` + `.claude/skills/` | ✅ 原生 |
| **Cursor** | `.cursorrules` + `.cursor/rules/` | ✅ 0.45+ |
| **Windsurf** | `.windsurfrules` + `.windsurf/skills/` | ✅ 原生 |
| **GitHub Copilot** | `.github/copilot-instructions.md` | ✅ |
| **Codex CLI** | `CLAUDE.md` + `.claude/skills/` | ✅ 兼容 |
| **Gemini CLI** | `GEMINI.md` + `.gemini/skills/` | ✅ 兼容 |
| **AGENTS.md** | 开放标准，20+ 工具支持 | ✅ 通用 |

### ✅ 精选 100+ 实用 Skills

- **15 个官方核心 Skills** — Anthropic 出品，质量最高
- **14 个 Superpowers 工作流** — 覆盖开发全流程
- **14 个 Example Skills** — 学习编写 Skill 的最佳参考
- **14 个社区精选 Skills** — 来自各大仓库的精华
- **30+ 领域分类 Skills** — 按前端/后端/数据/AI/测试/安全分类

### ✅ 拿来即用的 CLAUDE.md 模板

- React + TypeScript
- Python + FastAPI
- Node.js + Express
- Go
- Next.js 全栈

### ✅ 最佳实践 & 避坑指南

- 决策矩阵：什么时候用 CLAUDE.md / Skill / Hook / Subagent？
- 常见陷阱：CLAUDE.md 过大、Skill 职责过宽、不验证就提交
- 省钱技巧：Token 优化、模型选择、上下文管理

---

## 🗺️ 完整内容导航

| 章节 | 内容 | 适合谁 |
|------|------|--------|
| [一、生态概览](awesome-agentic-skills.md#一生态概览) | 各平台规则机制对比 | 所有人 |
| [三、决策矩阵](awesome-agentic-skills.md#三决策矩阵该用哪种机制) | CLAUDE.md vs Skill vs Hook vs Subagent 怎么选 | 初学者 |
| [四、快速上手](awesome-agentic-skills.md#四各平台快速上手) | 各平台安装配置实操 | 初学者 |
| [五、Skills 大全](awesome-agentic-skills.md#五claude-code-skills-大全) | 57 个 Claude Code Skills 详解 | Claude Code 用户 |
| [十三、CLAUDE.md 模板](awesome-agentic-skills.md#十三claudemd-模板可直接用) | 5 套项目模板直接复制 | 项目初始化 |
| [十四、最佳实践](awesome-agentic-skills.md#十四agent-skills-最佳实践) | 编写原则 + 质量自检清单 | Skill 作者 |
| [十五、避坑指南](awesome-agentic-skills.md#十五常见陷阱--避坑指南) | 6 个常见陷阱 + 解决方案 | 所有人 |

---

## 🤝 贡献指南

欢迎贡献！请遵循以下流程：

1. Fork 本仓库
2. 创建分支：`git checkout -b feat/add-skill-xxx`
3. 提交：`git commit -m "feat: add xxx skill"`
4. PR 到 main 分支

提交信息请遵循 [Conventional Commits](https://www.conventionalcommits.org/) 格式。

---

## 📦 推荐资源

| 资源 | 链接 | 说明 |
|------|------|------|
| 完整知识库 | [awesome-agentic-skills.md](awesome-agentic-skills.md) | 📖 必读 |
| antigravity-awesome-skills | [GitHub ⭐42k](https://github.com/sickn33/antigravity-awesome-skills) | 1,900+ Skills |
| VoltAgent/awesome-agent-skills | [GitHub ⭐27k](https://github.com/VoltAgent/awesome-agent-skills) | 官方团队出品 |
| Suede Creator Skills | [GitHub ⭐166](https://github.com/JasonColapietro/suede-creator-skills) | 面向 Claude Code 与 Codex 的 67 个 MIT 开源工作流 Skills |
| Claude Code 最佳实践 | [GitHub](https://github.com/MuhammadUsmanGM/claude-code-best-practices) | 项目模板 + 安全手册 |

---

## 📄 许可

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) — 自由使用、分享、演绎。
