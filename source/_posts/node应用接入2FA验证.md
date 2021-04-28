---
title: node应用接入2FA验证
tags:
  - node
  - server
  - node_modules
  - 2FA
originContent: ''
categories:
  - 记录
toc: true
date: 2021-04-28 13:22:29
---

## 参考链接

- [双因素认证（2FA）教程 - 阮一峰](https://www.ruanyifeng.com/blog/2017/11/2fa-tutorial.html)

## 何为 2FA 验证

- 双因素认证（Two-factor authentication，简称 2FA）
- 常见方案

  - 密码 + 某种个人物品，比如 U 盾，缺点：不方便
  - 密码 + 短信验证码， 缺点：不够安全，SIM 卡可以伪造、复制
  - 基于 TOTP
    - TOTP 的全称是"基于时间的一次性密码"（Time-based One-time Password）
    - 国际标准 [RFC6238](https://tools.ietf.org/html/rfc6238)

## 优缺点

### 优点

- 比单纯的密码登录安全得多。就算密码泄露，只要手机还在，账户就是安全的。

### 缺点

- 登录多了一步，费时且麻烦，用户会感到不耐烦
- 不意味着账户的绝对安全，入侵者依然可以通过盗取 cookie 或 token，劫持整个对话（session）
- 一旦忘记密码或者遗失手机，想要恢复登录，势必就要绕过双因素认证，这就形成了一个安全漏洞。除非准备两套双因素认证，一套用来登录，另一套用来恢复账户。

## node 应用如何接入 2FA 验证

### npm：[node-2fa](https://www.npmjs.com/package/node-2fa)

- 目前仍在更新维护
- 支持应用
  - Authy
  - Google Authenticator
  - Microsoft Authenticator
- 安装 `npm install node-2fa --save`

```js
const twofactor = require('node-2fa')

const newSecret = twofactor.generateSecret({
  name: 'My Awesome App',
  account: 'johndoe',
})
/*
{ secret: 'XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W',
  uri: 'otpauth://totp/My%20Awesome%20App:johndoe?secret=XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W&issuer=My%20Awesome%20App',
  qr: 'https://chart.googleapis.com/chart?chs=166x166&chld=L|0&cht=qr&chl=otpauth://totp/My%20Awesome%20App:johndoe%3Fsecret=XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W%26issuer=My%20Awesome%20App'
}
*/

const newToken = twofactor.generateToken('XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W')
// => { token: '630618' }

twofactor.verifyToken('XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W', '630618')
// => { delta: 0 }

twofactor.verifyToken('XDQXYCP5AC6FA32FQXDGJSPBIDYNKK5W', '00')
// => null
```

### npm：[2fa](https://www.npmjs.com/package/2fa)

- 缺点
  - 最后一次更新在 6 年前

> 记录完毕
