---
layout: post
title: "OpenClaw 安装与使用完整指南"
date: 2026-03-18
categories: 工具
tags: [OpenClaw, AI, 效率工具, 安装教程]
---

OpenClaw 是一个强大的 AI 助手框架，可以让你在各种平台上运行自己的 AI 助手。本文将详细介绍如何安装和使用 OpenClaw。

## 目录

- [什么是 OpenClaw](#什么是-openclaw)
- [安装要求](#安装要求)
- [安装方式](#安装方式)
- [首次配置](#首次配置)
- [基本使用](#基本使用)
- [Gateway 服务](#gateway-服务)
- [常见问题与解决方案](#常见问题与解决方案)
- [注意事项](#注意事项)

---

## 什么是 OpenClaw

OpenClaw 是一个开源的 AI 助手平台，支持：

- **多渠道接入**：Web Chat、Discord、Telegram、Signal、WhatsApp 等
- **多模型支持**：可以连接 OpenAI、Claude、GLM 等各种 AI 模型
- **技能系统**：通过 Skills 扩展功能，如 GitHub 操作、天气查询等
- **持久化记忆**：AI 可以记住之前的对话和重要信息
- **定时任务**：支持 Cron 和 Heartbeat 机制进行周期性检查

官网：[https://openclaw.ai](https://openclaw.ai)  
GitHub：[https://github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)

---

## 安装要求

### 系统要求

- **Node.js**：v18.0.0 或更高版本（推荐使用 nvm 管理）
- **npm**：随 Node.js 一起安装
- **Git**：用于克隆仓库和安装某些依赖
- **操作系统**：Windows、macOS、Linux 均支持

### 推荐环境配置

```bash
# 使用 nvm 安装 Node.js（推荐）
nvm install 20
nvm use 20

# 验证版本
node --version  # 应该显示 v20.x.x 或更高
npm --version
```

---

## 安装方式

### 方式一：npm 全局安装（推荐）

最简单的安装方式：

```bash
npm install -g openclaw
```

### 方式二：使用 npx（无需安装）

如果你想先试用，可以直接使用 npx：

```bash
npx openclaw
```

### 方式三：从源码安装

适合开发者或需要最新功能的用户：

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
npm install
npm link
```

### 验证安装

```bash
openclaw --version
# 输出示例：OpenClaw 2026.3.13 (61d171a)
```

---

## 首次配置

### 1. 初始化工作目录

```bash
openclaw init
```

这会创建 `~/.openclaw/` 目录，包含配置文件和工作空间。

### 2. 配置 AI 模型

编辑 `~/.openclaw/config.json`，添加你的 AI 模型 API：

```json
{
  "models": {
    "default": "your-model-provider/model-name"
  },
  "providers": {
    "openai": {
      "apiKey": "sk-xxx"
    },
    "anthropic": {
      "apiKey": "sk-ant-xxx"
    }
  }
}
```

### 3. 配置连接渠道（可选）

如果你想接入 Discord、Telegram 等平台，需要在配置文件中添加相应设置：

```json
{
  "channels": {
    "discord": {
      "token": "your-bot-token",
      "enabled": true
    },
    "telegram": {
      "token": "your-bot-token",
      "enabled": true
    }
  }
}
```

---

## 基本使用

### 启动交互式对话

```bash
openclaw chat
```

### 常用命令

```bash
# 查看帮助
openclaw help

# 查看状态
openclaw status

# 更新 OpenClaw
openclaw update

# 启动 Gateway 服务
openclaw gateway start

# 停止 Gateway 服务
openclaw gateway stop

# 查看 Gateway 状态
openclaw gateway status
```

### 工作目录结构

```
~/.openclaw/
├── config.json        # 主配置文件
├── workspace/         # 工作目录
│   ├── AGENTS.md      # Agent 行为指南
│   ├── SOUL.md        # AI 人格设定
│   ├── USER.md        # 用户信息
│   ├── MEMORY.md      # 长期记忆
│   ├── TOOLS.md       # 工具配置
│   ├── IDENTITY.md    # AI 身份信息
│   └── memory/        # 日常记忆存储
│       └── 2026-03-18.md
└── logs/              # 日志文件
```

---

## Gateway 服务

Gateway 是 OpenClaw 的后台服务，负责处理来自各渠道的消息。

### 启动 Gateway

```bash
# 前台运行（调试用）
openclaw gateway

# 后台服务模式
openclaw gateway start
```

### 管理 Gateway

```bash
# 查看状态
openclaw gateway status

# 停止服务
openclaw gateway stop

# 重启服务
openclaw gateway restart
```

### Gateway 的作用

- 监听配置的消息渠道（Discord、Telegram 等）
- 接收消息并转发给 AI 处理
- 管理 Cron 定时任务
- 处理 Heartbeat 心跳检查

---

## 常见问题与解决方案

### 问题 1：npm install 报 SSH 权限错误

**错误信息：**
```
npm error command git --no-replace-objects ls-remote ssh://git@github.com/...
npm error Permission denied (publickey)
```

**原因：** 某些依赖需要从 GitHub 克隆，但没有配置 SSH 密钥。

**解决方案：** 让 Git 使用 HTTPS 代替 SSH：

```bash
git config --global url."https://github.com/".insteadOf ssh://git@github.com/
```

### 问题 2：无法连接 GitHub

**错误信息：**
```
fatal: unable to access 'https://github.com/...': Failed to connect to github.com port 443
```

**原因：** 网络问题，可能需要代理。

**解决方案：**

1. 如果你使用代理，配置 Git 代理：

```bash
# 假设代理端口是 1080
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
```

2. 不需要代理时，可以取消：

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### 问题 3：更新时文件被占用（Windows）

**错误信息：**
```
npm error code EBUSY
npm error syscall rename
npm error path .../node_modules/openclaw
```

**原因：** Gateway 正在运行，文件被锁定。

**解决方案：** 先停止 Gateway 再更新：

```bash
openclaw gateway stop
openclaw update
openclaw gateway start
```

### 问题 4：Node.js 版本过低

**错误信息：**
```
error openclaw@x.x.x: The engine "node" is incompatible
```

**解决方案：** 升级 Node.js 到 v22 或更高版本：

```bash
# 使用 nvm
nvm install 22
nvm use 22
```

### 问题 5：npm 缓存问题

如果遇到奇怪的依赖问题，尝试清理缓存：

```bash
npm cache clean --force
```

---

## 注意事项

### ⚠️ 安全相关

1. **API Key 保护**：永远不要把 API Key 提交到公开仓库
2. **配置文件权限**：确保 `~/.openclaw/config.json` 只有你能读取
3. **代理设置**：使用代理时注意安全性，确保代理可信

### 💡 使用建议

1. **定期更新**：OpenClaw 活跃开发中，建议定期运行 `openclaw update`

2. **备份工作目录**：`~/.openclaw/workspace/` 包含你的记忆和配置，建议定期备份

3. **合理使用记忆功能**：
   - `MEMORY.md` 存储长期重要信息
   - `memory/YYYY-MM-DD.md` 记录日常事务
   - 敏感信息不要写入记忆文件

4. **Gateway 资源占用**：Gateway 会持续运行，如果不需要后台服务可以关闭

### 🌐 网络相关

1. **中国大陆用户**：
   - 某些依赖需要访问 GitHub，可能需要代理
   - AI 模型 API 可能需要稳定的国际网络连接

2. **代理配置时机**：
   - 安装/更新时：需要配置 Git 代理
   - 使用时：需要确保能访问 AI 模型 API

### 📁 文件系统

1. **工作目录**：默认在 `~/.openclaw/workspace/`，可以在配置中修改
2. **日志位置**：`~/.openclaw/logs/`，遇到问题时可以查看
3. **npm 缓存**：Windows 在 `%APPDATA%\npm-cache\_logs\`

---

## 进阶使用

### 自定义 AI 人格

编辑 `~/.openclaw/workspace/SOUL.md` 来定义 AI 的性格和行为方式。

### 添加技能（Skills）

OpenClaw 支持通过 Skills 扩展功能：

1. 从 [ClawHub](https://clawhub.com) 发现新技能
2. 将技能安装到 `~/.openclaw/skills/` 目录
3. 在配置中启用技能

### 配置定时任务

使用 Cron 或 Heartbeat 功能让 AI 定期执行任务：

```json
{
  "cron": {
    "jobs": [
      {
        "schedule": "0 9 * * *",
        "action": "每日早晨提醒"
      }
    ]
  }
}
```

---

## 相关资源

- 📖 [官方文档](https://docs.openclaw.ai)
- 💻 [GitHub 仓库](https://github.com/openclaw/openclaw)
- 💬 [Discord 社区](https://discord.com/invite/clawd)
- 🔌 [技能市场 ClawHub](https://clawhub.com)

---

## 总结

OpenClaw 是一个功能强大的 AI 助手平台，通过本文你应该能够：

1. ✅ 成功安装 OpenClaw
2. ✅ 配置 AI 模型和渠道
3. ✅ 解决常见的安装问题
4. ✅ 理解基本的使用方式

如果在安装或使用过程中遇到问题，可以：
- 查看本文的「常见问题与解决方案」部分
- 访问 [Discord 社区](https://discord.com/invite/clawd) 寻求帮助
- 在 [GitHub Issues](https://github.com/openclaw/openclaw/issues) 提交问题

---

*希望这篇指南对你有帮助！如有问题欢迎留言讨论。*
