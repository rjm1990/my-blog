---
layout: post
title: "代码重构的艺术：让代码更优雅的10个原则"
date: 2026-03-19
categories: 程序员发展
tags: [代码质量, 重构, 最佳实践]
---

重构不是重写，而是一种渐进式的改进。

## 🎯 什么时候该重构？

- 函数超过50行
- 嵌套超过3层
- 变量名看不懂
- 重复代码出现3次以上
- 添加新功能需要修改多个地方

## 💡 重构的10个原则

### 1. 小步前进
不要一次性改太多。每次只改一个小点，测试通过后再继续。

### 2. 保持测试覆盖
重构前确保有测试，重构后运行测试。没有测试的重构是赌博。

### 3. 提取函数
如果一个函数做了两件事，就拆成两个函数。

```javascript
// 重构前
function processOrder(order) {
  // 验证订单
  if (!order.items || order.items.length === 0) {
    return false;
  }
  // 计算总价
  let total = 0;
  order.items.forEach(item => {
    total += item.price * item.quantity;
  });
  // 保存订单
  database.save(order);
  // 发送邮件
  emailService.send(order.email, '订单确认');
}

// 重构后
function processOrder(order) {
  if (!validateOrder(order)) return false;
  const total = calculateTotal(order);
  saveOrder(order);
  sendConfirmationEmail(order);
}
```

### 4. 消除重复
DRY原则：Don't Repeat Yourself。重复的代码是bug的温床。

### 5. 有意义的命名
变量名要能表达意图，不要用 `temp`, `data`, `info` 这种模糊的名字。

### 6. 减少参数
函数参数超过3个，就该考虑封装成对象了。

### 7. 用多态替代条件
过多的 if-else 是代码坏味道，考虑用策略模式或多态替代。

### 8. 分解大函数
超过50行的函数，大概率可以拆分。

### 9. 消除魔法数字
不要直接写数字，用常量代替。

```javascript
// 不好
if (user.age >= 18) { ... }

// 好
const ADULT_AGE = 18;
if (user.age >= ADULT_AGE) { ... }
```

### 10. 保持简单
KISS原则：Keep It Simple, Stupid。能用简单方法解决的问题，不要过度设计。

## 🚫 重构的误区

- **重构≠重写**：重构是渐进式的，重写是推倒重来
- **重构≠性能优化**：重构是为了可读性和可维护性
- **重构不是炫技**：不要为了用设计模式而用设计模式

## 📚 推荐阅读

- 《重构：改善既有代码的设计》- Martin Fowler
- 《代码整洁之道》- Robert C. Martin

---

*你最近重构了什么代码？欢迎分享你的经验！*
