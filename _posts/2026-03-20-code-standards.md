---
layout: post
title: "代码规范与团队协作：如何写出团队友好的代码"
date: 2026-03-20
categories: 程序员发展
tags: [代码规范, 团队协作, 代码质量]
---

代码是写给人看的，顺便给机器执行。

## 🎯 代码规范的意义

### 对个人

- 代码更易读
- 减少低级错误
- 提升编码效率

### 对团队

- 降低沟通成本
- 方便代码review
- 新人更容易上手

### 对项目

- 提高可维护性
- 减少bug
- 降低技术债

## 📋 常见代码规范

### 命名规范

**原则：名副其实**

```javascript
// ❌ 不好
let d; // elapsed time in days
let list = ['a', 'b'];
let flag = true;

// ✅ 好
let elapsedTimeInDays;
let fruits = ['apple', 'banana'];
let isValid = true;
```

**命名风格**

```javascript
// 变量：小驼峰
let userName = 'John';

// 常量：全大写下划线
const MAX_RETRY_COUNT = 3;

// 函数：动词开头
function getUserInfo() {}
function calculateTotal() {}
function isValidEmail() {}

// 类：大驼峰
class UserService {}

// 私有属性：下划线开头
class User {
  constructor() {
    this._privateField = 1;
  }
}

// 文件名：小写中划线
user-service.js
```

### 函数规范

**原则：单一职责**

```javascript
// ❌ 不好：一个函数做多件事
function processOrder(order) {
  // 验证
  if (!order.items) return false;
  // 计算
  let total = 0;
  // 保存
  database.save(order);
  // 发邮件
  emailService.send(order);
}

// ✅ 好：一个函数做一件事
function processOrder(order) {
  if (!validateOrder(order)) return false;
  const total = calculateTotal(order);
  saveOrder(order);
  sendConfirmationEmail(order);
}
```

**参数控制**

```javascript
// ❌ 不好：参数太多
function createUser(name, email, age, phone, address, city) {}

// ✅ 好：使用对象参数
function createUser(userInfo) {
  const { name, email, age, phone, address, city } = userInfo;
}

// ✅ 好：设置默认值
function fetchData(url, options = {}) {
  const { method = 'GET', headers = {} } = options;
}
```

**函数长度**

- 建议：不超过50行
- 如果超过：考虑拆分

### 注释规范

**原则：注释说明为什么，不是做什么**

```javascript
// ❌ 不好：废话注释
// 获取用户名
function getUserName() {
  return this.userName;
}

// ❌ 不好：过时的注释
// 计算总价（实际上在计算折扣）
function calculateTotal() {
  return this.price * 0.8;
}

// ✅ 好：解释为什么
// 使用小数点后两位截断，避免浮点数精度问题
function formatPrice(price) {
  return Math.floor(price * 100) / 100;
}

// ✅ 好：TODO注释
// TODO: 后续需要支持多语言
function formatDate(date) {
  return date.toLocaleDateString();
}
```

### 代码格式

**缩进**

```javascript
// 使用2空格或4空格，团队统一
if (true) {
  doSomething();
}
```

**空行**

```javascript
// 函数之间空一行
function foo() {
  // ...
}

function bar() {
  // ...
}

// 逻辑块之间空一行
function process() {
  // 初始化
  const data = loadData();
  
  // 处理
  const result = transform(data);
  
  // 返回
  return result;
}
```

**行宽**

- 建议：不超过80-120字符
- 过长的行要换行

## 🛠️ 规范工具

### ESLint

```javascript
// .eslintrc.js
module.exports = {
  extends: ['eslint:recommended'],
  rules: {
    'no-unused-vars': 'error',
    'prefer-const': 'warn',
    'no-var': 'error',
  },
};
```

### Prettier

```javascript
// .prettierrc
{
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100
}
```

### Git Hooks

```javascript
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.js": ["eslint --fix", "prettier --write"]
  }
}
```

## 📊 团队规范制定

### 规范内容

```markdown
## 代码规范

### 1. 命名规范
- 变量：小驼峰
- 常量：全大写
- 类：大驼峰

### 2. 函数规范
- 单一职责
- 不超过50行
- 参数不超过3个

### 3. 注释规范
- 必须注释复杂逻辑
- 使用JSDoc

### 4. Git规范
- commit message格式
- PR流程
- 代码review要求
```

### 规范落地

1. **文档化**: 写成文档，放在仓库
2. **工具化**: 用ESLint/Prettier自动检查
3. **流程化**: PR必须经过review
4. **持续化**: 定期review和更新

## 🚫 常见反模式

### 1. 魔法数字

```javascript
// ❌
if (status === 1) { }

// ✅
const STATUS_ACTIVE = 1;
if (status === STATUS_ACTIVE) { }
```

### 2. 嵌套过深

```javascript
// ❌
if (a) {
  if (b) {
    if (c) {
      // ...
    }
  }
}

// ✅
if (!a) return;
if (!b) return;
if (!c) return;
// ...
```

### 3. 函数过长

```javascript
// ❌ 一个函数500行

// ✅ 拆成多个小函数
function main() {
  const data = prepare();
  const result = process(data);
  cleanup();
  return result;
}
```

## 💡 Code Review要点

### 审查者

- 关注设计合理性
- 关注可读性
- 关注潜在bug
- 不要纠结个人偏好

### 被审查者

- 代码先自测
- PR描述清楚
- 控制PR大小
- 虚心接受建议

## 📚 推荐阅读

- 《代码整洁之道》
- 《编写可读代码的艺术》
- 《重构》

---

*好的代码自己会说话。*
