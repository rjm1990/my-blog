---
layout: post
title: "Git提交的艺术：写出让人看懂的commit message"
date: 2026-03-19
categories: 程序员发展
tags: [Git, 团队协作, 最佳实践]
---

一个好的commit message，能让队友少骂你几句。

## 😤 糟糕的提交信息

```
- 修改了
- fix bug
- update
- 完成了功能
- wip
- 。。。
```

这些提交信息，过两周你自己都看不懂。

## ✅ 好的提交信息长这样

### 格式规范

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type类型

- **feat**: 新功能
- **fix**: 修复bug
- **docs**: 文档修改
- **style**: 代码格式（不影响逻辑）
- **refactor**: 重构
- **test**: 测试相关
- **chore**: 构建/工具相关
- **perf**: 性能优化

### 实际例子

```
feat(用户模块): 添加邮箱验证功能

- 添加邮箱格式验证
- 添加邮箱唯一性检查
- 添加邮箱验证码发送

Closes #123
```

```
fix(订单模块): 修复订单金额计算错误

问题：订单金额在小数点后两位时计算错误
原因：浮点数精度问题
解决：使用decimal类型存储金额

Fixes #456
```

## 💡 写好commit message的技巧

### 1. 使用祈使句
用 "添加功能" 而不是 "添加了功能"

### 2. 首行不超过50字符
太长的标题在小屏幕上显示不全

### 3. 说明为什么，而不是做了什么
代码本身能说明做了什么，commit message应该说明为什么这么做

### 4. 一个提交只做一件事
不要把多个不相关的修改放在一个commit里

### 5. 提交前review自己的diff
确保提交的内容和message描述一致

## 🛠️ 工具推荐

- **commitizen**: 交互式提交工具
- **husky**: Git hooks工具
- **commitlint**: 提交信息检查工具

```bash
# 安装commitizen
npm install -g commitizen
cz  # 替代 git commit
```

## 📊 团队规范示例

```yaml
# .commitlintrc.yml
extends:
  - '@commitlint/config-conventional'
rules:
  type-enum:
    - 2
    - always
    - - feat
      - fix
      - docs
      - style
      - refactor
      - test
      - chore
```

---

*好的commit message是对队友的尊重，也是对未来的自己负责。*
