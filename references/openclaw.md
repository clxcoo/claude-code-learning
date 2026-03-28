# OpenClaw 完整学习指南

## 环境要求

- **Node.js**: 22.12.0+
- **AI 模型**: OpenAI / Anthropic / Google / Ollama
- **操作系统**: macOS / Linux / Windows (推荐 WSL2)

---

## 安装部署

### 方式一：直接安装

```bash
# 克隆项目
git clone https://github.com/peter-clawdbot/openclaw.git
cd openclaw

# 安装依赖
npm install

# 配置环境变量
cp .env.example .env
```

### 方式二：Docker 部署

```bash
# 构建镜像
docker build -t openclaw .

# 运行容器
docker run -d -p 3000:3000 --env-file .env openclaw
```

### 环境变量配置

```bash
# 必需：至少配置一个 AI 模型
OPENAI_API_KEY="sk-..."
ANTHROPIC_API_KEY="sk-ant-..."
GOOGLE_API_KEY="..."
OLLAMA_HOST="http://localhost:11434"

# 可选：消息平台
TELEGRAM_BOT_TOKEN="..."
DISCORD_BOT_TOKEN="..."
WHATSAPP_SESSION_PATH="..."
```

---

## 快速开始

### Step 1: 配置 AI 模型

编辑 `agents.yaml`：

```yaml
models:
  - provider: openai
    model: gpt-4
    apiKey: ${OPENAI_API_KEY}
```

### Step 2: 启动服务

```bash
npm start
```

### Step 3: 连接消息平台

根据需要配置 Telegram/Discord/WhatsApp 等平台。

---

## 支持的 AI 模型（29个）

| 提供商 | 模型示例 |
|--------|----------|
| OpenAI | gpt-4, gpt-4-turbo, gpt-3.5-turbo |
| Anthropic | claude-3-opus, claude-3-sonnet |
| Google | gemini-pro, gemini-ultra |
| Ollama | llama2, mistral, codellama |
| Azure OpenAI | gpt-4 Azure |
| 等等 | ... |

### 配置示例

```yaml
models:
  - provider: anthropic
    model: claude-3-opus-20240229
    apiKey: ${ANTHROPIC_API_KEY}
```

---

## 消息平台集成（15+）

| 平台 | 配置项 |
|------|--------|
| Telegram | TELEGRAM_BOT_TOKEN |
| Discord | DISCORD_BOT_TOKEN |
| WhatsApp | WHATSAPP_SESSION_PATH |
| 飞书 | FEISHU_APP_ID, FEISHU_APP_SECRET |
| Slack | SLACK_BOT_TOKEN |
| Microsoft Teams | TEAMS_APP_ID |

### Telegram 配置

```bash
# 替换为你的 Bot Token
TELEGRAM_BOT_TOKEN="YOUR_BOT_TOKEN_HERE"
```

### Discord 配置

```bash
# 替换为你的 Bot Token
DISCORD_BOT_TOKEN="YOUR_BOT_TOKEN_HERE"
```

---

## 技能系统

### 内置技能（50+）

- `web-search` - 网页搜索
- `wikipedia` - 维基百科查询
- `weather` - 天气查询
- `calculator` - 数学计算
- ` reminder` - 提醒设置
- 等等...

### 自定义技能

在 `skills/` 目录创建：

```yaml
name: my-skill
description: 自定义技能说明
triggers:
  - "帮我查天气"
actions:
  - type: http
    url: "https://api.weather.com/v1"
```

---

## 记忆系统

### 自动记忆

OpenClaw 自动保存对话到 `memory/` 目录：

```markdown
# memory/users/{user_id}.md

## 对话摘要
[AI自动生成]

## 用户偏好
- 语言: 中文
- 偏好: ...
```

### 刷新记忆

```bash
# 手动刷新
/openmemory refresh
```

---

## 多 Agent 协作

### 配置多个 Agent

```yaml
agents:
  - name: assistant
    model: gpt-4
    skills: [web-search, calculator]

  - name: coder
    model: claude-3-opus
    skills: [code-review]
```

### 消息路由

```yaml
routing:
  - pattern: "写代码/*"
    agent: coder
  - pattern: "其他/*"
    agent: assistant
```

---

## 安全配置

### Gateway Token

```bash
# 设置 Gateway 访问令牌
GATEWAY_TOKEN="your-secure-token"
```

### TLS 配置

```bash
# 启用 TLS 1.3
TLS_ENABLED=true
TLS_CERT_PATH="/path/to/cert"
TLS_KEY_PATH="/path/to/key"
```

### 权限管理

```yaml
permissions:
  - user: user1
    allowedActions: [chat, search]
  - user: user2
    allowedActions: [chat]
```

---

## 故障排查

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| 连接平台失败 | 检查 Token 配置 |
| AI 模型不响应 | 验证 API Key |
| 消息发不出去 | 检查平台权限 |
| Docker 运行失败 | 检查端口占用 |

### 日志查看

```bash
# 查看实时日志
npm run logs

# 调试模式
DEBUG=* npm start
```

---

## 部署方案

### 本地部署

直接运行，适合开发测试。

### VPS 部署

```bash
# 使用 PM2 保持运行
pm2 start npm --name openclaw -- start
```

### Fly.io / Render

参考官方部署文档。

---

## 学习资源

- 官方文档：https://openclaw.com
- 教程仓库：https://github.com/KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh
