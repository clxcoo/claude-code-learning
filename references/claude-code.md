# Claude Code 完整学习指南

## 环境要求

- **操作系统**：Windows 10+、macOS 10.15+、Linux
- **API Key**：Anthropic API 密钥（或第三方中转站）
- **IDE**：VS Code、Cursor、Windsurf

> ⚠️ 2026年更新：Claude Code 已原生安装，无需 Node.js

---

## 安装步骤

### Step 1: 获取 API Key

1. 访问 [Anthropic Console](https://console.anthropic.com/)
2. 创建账户并获取 API Key
3. （可选）配置中转站 API 降低成本

### Step 2: 安装 Claude Code

**macOS/Linux:**
```bash
curl -fsSL https://anthropic.com/claude/claude.sh | sh
```

**Windows:**
```powershell
winget install Anthropic.Claude
```

### Step 3: 首次配置

```bash
claude
# 按提示输入 API Key
```

### 环境变量配置

```bash
# API Key
export ANTHROPIC_API_KEY="YOUR_API_KEY_HERE"

# 或使用中转站
export ANTHROPIC_BASE_URL="https://api.example.com/v1"
```

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
claude --model opus "复杂任务"

# 工作树模式（隔离任务）
claude -w "新功能分支"
```

### Slash 命令

| 命令 | 功能 |
|------|------|
| `/help` | 显示帮助 |
| `/compact` | 压缩上下文 |
| `/resume` | 恢复会话 |
| `/voice` | 语音输入 |
| `/fast` | 快速模式 |
| `/effort` | 推理深度 |
| `/loop` | 循环执行 |

---

## MCP 集成

MCP (Model Context Protocol) 扩展 Claude 能力。

### 配置 MCP

在项目 `CLAUDE.md` 中配置：

```markdown
## MCP Servers

- filesystem:
  - command: npx -y @modelcontextprotocol/server-filesystem .
  - args: ["/path/to/dir"]

- memory:
  - command: npx -y @modelcontextprotocol/server-memory
```

### 常用 MCP 服务器

| 服务器 | 功能 |
|--------|------|
| filesystem | 文件系统访问 |
| memory | 持久化记忆 |
| github | GitHub 操作 |
| puppeteer | 浏览器自动化 |
| sqlite | 数据库操作 |

---

## Hooks 系统

Hooks 在特定事件触发时执行脚本。

### 配置 Hooks

在 `CLAUDE.md` 中：

```markdown
## Hooks

on:
  - trigger: PreTask
    run: ./scripts/pre_task.sh

  - trigger: Notification
    run: ./scripts/notify.sh
```

### Hook 类型

| 类型 | 触发时机 |
|------|----------|
| PreTask | 任务开始前 |
| PostTask | 任务完成后 |
| Notification | 通知事件 |
| StopFailure | 执行失败时 |

---

## Subagent 子代理

专业任务的子代理专家。

### 内置子代理

```
general-purpose  - 通用任务
Explore         - 代码探索
CodeReview      - 代码审查
Task            - 任务执行
```

### 自定义子代理

在 `CLAUDE.md` 中配置：

```markdown
## Subagents

- name: my-agent
  description: 处理特定任务
  prompt: |
    你是一个...
```

---

## Skills 自定义技能

创建可复用功能包。

### Skill 结构

```
skill-name/
├── SKILL.md (必需)
└── scripts/ (可选)
    └── *.py, *.sh
```

### SKILL.md 格式

```markdown
---
name: my-skill
description: 技能描述和触发条件
---

# 技能说明

[使用说明]
```

### 使用技能

```bash
claude /skill-name
```

---

## 企业级配置

### modelOverrides（企业端点）

```markdown
## modelOverrides

- model: claude-opus-4-6
  apiURL: https://api.company.com/v1

- model: claude-sonnet-4-6
  apiURL: https://api.company.com/v1
```

### Worktree（大项目优化）

```bash
# 并行任务隔离
claude -w feature-branch
```

---

## 故障排查

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| API Key 无效 | 检查 Key 是否过期 |
| 连接超时 | 配置代理或中转站 |
| 权限不足 | 使用 `--permissions` 参数 |
| MCP 不工作 | 检查 Node.js 和配置格式 |

### 日志调试

```bash
# 启用调试
claude --verbose
```

---

## 学习资源

- 官方文档：https://docs.anthropic.com
- 教程仓库：https://github.com/KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh
