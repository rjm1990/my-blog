---
layout: post
title: "程序员的工作效率：打造高效的开发环境"
date: 2026-03-20
categories: 程序员发展
tags: [效率, 工具, 开发环境]
---

工欲善其事，必先利其器。

## ⌨️ 键盘快捷键

### 必会快捷键

**通用**
```
Ctrl+C/V/X  复制/粘贴/剪切
Ctrl+Z      撤销
Ctrl+S      保存
Ctrl+F      查找
Ctrl+A      全选
```

**编辑器（VS Code）**
```
Ctrl+D          选中下一个相同词
Ctrl+Shift+K    删除整行
Alt+Up/Down     移动行
Ctrl+/          注释/取消注释
Ctrl+P          快速打开文件
Ctrl+Shift+P    命令面板
F12             跳转到定义
Ctrl+B          切换侧边栏
```

**浏览器**
```
F12             开发者工具
Ctrl+Shift+I    开发者工具
Ctrl+L          选中地址栏
Ctrl+T          新标签页
Ctrl+W          关闭标签页
```

**每天省1小时，一年省365小时**

## 🛠️ 编辑器配置

### VS Code必装插件

**开发必备**
- ESLint: 代码规范检查
- Prettier: 代码格式化
- GitLens: Git增强
- Auto Rename Tag: 自动重命名标签
- Bracket Pair Colorizer: 括号着色

**效率提升**
- Path Intellisense: 路径补全
- Code Spell Checker: 拼写检查
- TODO Highlight: TODO高亮
- Live Server: 本地服务器

**主题**
- One Dark Pro
- Material Theme
- Dracula Official

### 配置优化

```json
{
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,
  "editor.minimap.enabled": false,
  "files.autoSave": "afterDelay",
  "workbench.colorTheme": "One Dark Pro"
}
```

## 🖥️ 终端工具

### 推荐终端

**Mac**
- iTerm2
- Warp

**Windows**
- Windows Terminal
- PowerShell 7

**Linux**
- Alacritty
- Kitty

### Shell配置

**Oh My Zsh**
```bash
# 安装
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 主题
ZSH_THEME="agnoster"

# 插件
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

### 常用别名

```bash
# Git
alias gs="git status"
alias ga="git add ."
alias gc="git commit -m"
alias gp="git push"
alias gl="git log --oneline"

# 项目
alias nr="npm run"
alias ns="npm start"
alias nt="npm test"

# 目录
alias ..="cd .."
alias ...="cd ../.."
alias home="cd ~"
alias work="cd ~/workspace"
```

## 📋 代码片段

### VS Code Snippets

```json
{
  "Console Log": {
    "prefix": "cl",
    "body": ["console.log($1);"],
    "description": "Console log"
  },
  "React Component": {
    "prefix": "rc",
    "body": [
      "import React from 'react';",
      "",
      "const ${1:Component} = () => {",
      "  return (",
      "    <div>",
      "      $2",
      "    </div>",
      "  );",
      "};",
      "",
      "export default ${1:Component};"
    ]
  }
}
```

### 全局片段工具

- **snippetsLab** (Mac)
- **massCode** (跨平台)
- **GistBox**

## 🔧 自动化脚本

### 项目初始化

```bash
#!/bin/bash
# init-project.sh

mkdir -p src/{components,utils,assets}
touch src/index.js
touch README.md
git init
npm init -y
echo "Project initialized!"
```

### 自动部署

```bash
#!/bin/bash
# deploy.sh

npm run build
rsync -avz dist/ user@server:/var/www/html/
echo "Deployed!"
```

### 定时任务

```bash
# 每天备份
0 2 * * * /path/to/backup.sh
```

## 📊 效率工具

### 任务管理

- **Todoist**: 待办清单
- **Notion**: 知识管理
- **TickTick**: 番茄钟+待办

### 时间追踪

- **Toggl**: 时间记录
- **RescueTime**: 自动追踪
- **WakaTime**: 编码时间统计

### 笔记工具

- **Notion**: 全能笔记
- **Obsidian**: 双链笔记
- **Logseq**: 大纲笔记

### 剪贴板管理

- **Alfred** (Mac)
- **utools** (跨平台)
- **Ditto** (Windows)

## 💡 效率提升技巧

### 1. 减少上下文切换

- 关闭不必要的通知
- 一次只做一件事
- 批量处理类似任务

### 2. 善用模板

```
项目模板
├── README.md
├── package.json
├── src/
├── tests/
└── .gitignore
```

### 3. 自动化重复工作

- 代码格式化：Prettier
- 代码检查：ESLint
- 测试运行：Jest watch
- 构建：Webpack/Vite

### 4. 保持专注

- 番茄工作法
- 关闭IM通知
- 戴降噪耳机

## 🖥️ 硬件推荐

### 显示器

- 双显示器：代码+预览
- 分辨率：至少1080p，推荐4K
- 尺寸：27寸比较合适

### 键盘

- 机械键盘：码字更舒服
- 紧凑布局：节省空间
- 蓝牙：减少线缆

### 鼠标

- 垂直鼠标：减少手腕压力
- 无线：更自由

### 椅子

- 人体工学椅：保护腰椎
- 值得投资

## 📱 移动办公

### 必备App

- **Working Copy**: iOS Git客户端
- **Termius**: SSH客户端
- **GitHub**: 移动端GitHub
- **Notion**: 笔记同步

### iPad开发

- **Swift Playgrounds**: 写Swift
- **Blink Shell**: 终端
- **Code Server**: 浏览器VS Code

## ⏰ 每日效率流程

```
08:50  打开电脑，查看今日任务
09:00  开始深度工作（关闭通知）
11:00  处理邮件、消息
12:00  午餐、休息
13:30  继续工作
15:00  站起来活动
17:00  整理今日工作，规划明日
18:00  下班
```

## 📊 效率自检

每周问自己：

- [ ] 这周学到了新快捷键吗？
- [ ] 重复性的工作能自动化吗？
- [ ] 工具配置还能优化吗？
- [ ] 时间都花在哪里了？

---

*效率提升是持续的过程，不是一次性的。*
