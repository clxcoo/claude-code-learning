---
name: claude-code-learning
description: |
  Claude Code 与 OpenClaw 互动学习指南。基于 KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh 教程，
  帮助零基础用户系统学习 AI 编程工具。包含 Claude Code 编程工作流和 OpenClaw 助手工作流的双线学习路径。
  适用场景：首次接触 Claude Code、想学习 AI 编程工具的小白、需要安装配置指导
metadata:
  author: claude-code-learning
  version: 1.0.0
  title: Claude Code 与 OpenClaw 学习指南
  description_zh: 零基础入门 Claude Code 和 OpenClaw 的互动学习技能，含避坑指南和实际案例
  tags:
    - claude-code
    - openclaw
    - 学习
    - 入门教程
    - AI工具
  license: MIT
---

# Claude Code 与 OpenClaw 互动学习指南

## 快速导航

| 学习目标 | 推荐路径 |
|----------|----------|
| 想学编程 AI | Part 1 Claude Code |
| 想玩 AI 助手 | Part 2 OpenClaw |
| 都想学 | 先 Claude Code 3小时 → 再 OpenClaw 1小时 |

---

## When to Use / When NOT to Use

### ✅ When to Use

- 首次接触 Claude Code，需要安装指导
- 不知道如何配置 API Key
- 想学习 MCP、Hooks、Skills 等扩展功能
- 想了解 OpenClaw 并搭建私人 AI 助手
- 遇到安装或使用问题需要排查

### ❌ When NOT to Use

- 已经是 Claude Code 高级用户 → 请使用 Agent-SDK 技能
- 需要企业级部署方案 → 请使用企业实战指南
- 只想问单个技术问题 → 直接提问即可

---

## Part 1: Claude Code 编程线

### 核心概念速查

| 概念 | 说明 | 复杂度 |
|------|------|--------|
| Claude Code | Anthropic 官方 AI 编程 CLI 工具 | ⭐ |
| MCP | Model Context Protocol，扩展能力 | ⭐⭐ |
| Hooks | 自动化工作流触发器 | ⭐⭐ |
| Skills | 可复用的功能包 | ⭐⭐ |
| Subagent | 子代理，专业任务专家 | ⭐⭐⭐ |

### 学习路径（3小时上手）

```text
Step 1（60分钟）：安装 → 基础使用
Step 2（30分钟）：MCP 集成
Step 3（30分钟）：Hooks 系统
完成 ✅ 会用 Claude Code + MCP + Hook
```

---

## 安装配置（避坑指南）

### 环境要求

| 项目 | 要求 | 备注 |
|------|------|------|
| 操作系统 | Windows 10+ / macOS 10.15+ / Linux | |
| API Key | Anthropic API 或中转站 | 国内用 MiniMax/硅基流动等 |
| IDE | VS Code / Cursor / Windsurf | 可选 |

> ⚠️ **2026年更新**：Claude Code 已原生安装，**无需 Node.js**

---

### ❌ 常见错误与解决方案

| 错误现象 | 可能原因 | 解决方案 |
|----------|----------|----------|
| `claude: command not found` | 安装未生效 | 重启终端或重新安装 |
| `API Key 无效` | Key 过期或格式错误 | 检查 Key 格式（sk-ant-开头） |
| `连接超时` | 网络问题/被墙 | 配置代理或使用中转站 |
| `权限不足` | 未授权操作 | 使用 `--permissions plan` |
| MCP 不工作 | Node.js 问题 | 确保 Node.js 18+ |

---

### API 中转站配置（国内用户必看）

**为什么要用中转站？**
- 国内直接访问 Anthropic API 可能不稳定
- 中转站可降低成本，支持 MiniMax/硅基流动等

**配置步骤：**

```powershell
# 临时设置（每次打开新终端）
$env:ANTHROPIC_BASE_URL = "https://api.minimax.chat/v1"
$env:ANTHROPIC_API_KEY = "你的MiniMax-API-Key"
claude
```

**常见中转站**：

| 中转站 | BASE_URL | 说明 |
|--------|----------|------|
| MiniMax | `https://api.minimax.chat/v1` | 需要 MiniMax API Key |
| 硅基流动 | `https://api.siliconflow.cn/v1` | 支持多种模型 |
| OpenRouter | `https://openrouter.ai/api/v1` | 聚合多个提供商 |

> ✅ **正确做法**：先测试单次请求确认中转站可用再正式使用
> ❌ **错误做法**：直接配置大量请求后发现不可用

---

## 基础使用

### 交互模式

```bash
claude
# 进入对话界面，输入问题
```

### 命令行模式

```bash
# 单次请求
claude -p "写一个Python冒泡排序"

# 指定模型
claude --model sonnet "复杂任务"

# 工作树模式（隔离任务）
claude -w "新功能分支"
```

### Slash 命令速查

| 命令 | 功能 | 场景 |
|------|------|------|
| `/help` | 显示帮助 | 忘记命令时 |
| `/compact` | 压缩上下文 | 对话太长时 |
| `/resume` | 恢复会话 | 重新开始 |
| `/voice` | 语音输入 | 不想打字时 |
| `/fast` | 快速模式 | 简单任务省token |
| `/effort` | 推理深度 | 复杂/简单任务 |
| `/loop` | 循环执行 | 重复任务 |

---

## 实际案例

### 案例1：首次安装验证

**场景**：用户首次安装 Claude Code，需要验证是否正常工作

**操作步骤**：

```powershell
# 1. 安装完成后验证版本
claude -v

# 2. 配置 API Key（首次）
$env:ANTHROPIC_API_KEY = "sk-ant-你的Key"
$env:ANTHROPIC_BASE_URL = "你的中转站URL"

# 3. 启动并测试
claude
# 输入：你好，请告诉我你的版本号
```

**预期结果**：
- 版本号显示（如 2.1.86）
- AI 正常回复

**❌ 失败情况**：
- `API Key 无效` → 检查 Key 是否正确
- `连接超时` → 检查网络/代理

---

### 案例2：MCP 服务器配置

**场景**：用户想用文件系统 MCP 访问项目文件

**配置方法**：

在项目根目录 `CLAUDE.md` 中添加：

```markdown
## MCP Servers

- filesystem:
  - command: npx -y @modelcontextprotocol/server-filesystem .
  - args: ["D:/my-project"]
```

**验证方法**：
```bash
claude
# 输入：列出当前目录的文件
```

**❌ 常见问题**：
- MCP 不响应 → 检查 npx 是否可用
- 权限被拒 → 确保路径正确且有权限

---

### 案例3：Hooks 自动化

**场景**：用户想在任务完成后自动发送通知

**配置方法**：

在 `CLAUDE.md` 中添加：

```markdown
## Hooks

on:
  - trigger: PostTask
    run: powershell -File ./notify.ps1
```

创建 `notify.ps1`：
```powershell
Write-Host "任务完成！"
```

**Before/After 对比**：

| 场景 | Before（手动） | After（自动） |
|------|----------------|---------------|
| 通知 | 任务完成后手动发送 | 自动触发 |
| 记录 | 手动记录日志 | Hook 自动记录 |
| 格式化 | 手动格式化代码 | Hook 自动格式化 |

---

## Part 2: OpenClaw 助手线

### 核心概念

| 概念 | 说明 | 复杂度 |
|------|------|--------|
| OpenClaw | 开源 AI 助手框架（224K+ Stars） | ⭐ |
| Skills | 50+ 内置技能 | ⭐⭐ |
| Memory | Markdown 记忆文件 | ⭐⭐ |
| Agent Teams | 多 Agent 协作 | ⭐⭐⭐ |

### 学习路径（1小时上手）

```text
Step 1（15分钟）：了解项目
Step 2（20分钟）：环境安装
Step 3（10分钟）：跑起第一个对话
Step 4（15分钟）：接入 AI 模型
```

---

## OpenClaw 安装（避坑指南）

### 环境要求

| 项目 | 要求 | 备注 |
|------|------|------|
| Node.js | 22.12.0+ | 必须使用 LTS 版本 |
| AI 模型 | OpenAI/Claude/Google/Ollama | 至少配置一个 |
| 操作系统 | macOS/Linux/Windows(WSL2) | 推荐 WSL2 |

> ⚠️ **注意**：Windows 原生支持较差，**推荐使用 WSL2**

---

### ❌ 常见错误

| 错误 | 解决方案 |
|------|----------|
| `npm install` 失败 | 检查 Node.js 版本是否是 22.12.0+ |
| 平台连接失败 | 检查 Token 配置是否正确 |
| 模型不响应 | 验证 API Key 有效性 |
| 端口被占用 | 更换端口或关闭占用程序 |

---

### 快速开始案例

**场景**：用户想在 5 分钟内跑通 OpenClaw

**Step 1：克隆项目**
```bash
git clone https://github.com/peter-clawdbot/openclaw.git
cd openclaw
```

**Step 2：安装依赖**
```bash
npm install
```

**Step 3：配置环境变量**
```bash
cp .env.example .env
# 编辑 .env，添加 API Key
```

**Step 4：启动**
```bash
npm start
```

**验证**：
- 看到 `Server running on port 3000` 即成功
- 访问 http://localhost:3000

---

## 支持的平台与模型

### AI 模型（29个）

| 提供商 | 模型示例 | 配置Key |
|--------|----------|---------|
| OpenAI | gpt-4, gpt-4-turbo | OPENAI_API_KEY |
| Anthropic | claude-3-opus | ANTHROPIC_API_KEY |
| Google | gemini-pro | GOOGLE_API_KEY |
| Ollama | llama2(本地) | OLLAMA_HOST |

### 消息平台（15+）

| 平台 | 配置项 | 难度 |
|------|--------|------|
| Telegram | TELEGRAM_BOT_TOKEN | ⭐ |
| Discord | DISCORD_BOT_TOKEN | ⭐ |
| WhatsApp | WHATSAPP_SESSION_PATH | ⭐⭐ |
| 飞书 | FEISHU_APP_ID | ⭐⭐ |

---

## 学习资源

| 资源 | 地址 |
|------|------|
| 完整教程 | https://github.com/KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh |
| Claude Code 官方 | https://docs.anthropic.com |
| OpenClaw 官方 | https://openclaw.com |
| 42plugin 社区 | https://42plugin.com |

---

## Quick Index

| 问题 | 快速查找 |
|------|----------|
| 不会安装 | 查看「安装配置」章节 |
| API Key 问题 | 查看「API 中转站配置」 |
| 遇到错误 | 查看「❌ 常见错误与解决方案」 |
| 想快速上手 | 查看「学习路径」 |
| 想用 OpenClaw | 查看「Part 2」 |
