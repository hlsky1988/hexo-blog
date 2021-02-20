---
title: 如何使用微软的API
tags:
  - 微软
  - API
categories:
  - API
toc: false
date: 2021-02-20 16:54:50
---

#### 起因

一直想做个 TODO 的展板放在桌面上，自己又懒不愿意从头开始写，要求又多，经人提醒可以尝试调用 Microsoft Todo 的数据，又有多端的APP可以用，尝试可行

#### 授权 - Microsoft Graph

> Microsoft Graph 是 Microsoft 365 中通往数据和智能的网关。 它提供统一的可编程模型，可用于访问 Microsoft 365、Windows 10 和企业移动性 + 安全性中的海量数据。 利用 Microsoft Graph 中的大量数据针对与数百万名用户交互的组织和客户构建应用。

[Microsoft Graph 文档地址](https://docs.microsoft.com/zh-cn/graph/overview)

> 需要注意：

1. 接口需要用户授权 （访问令牌）
2. 需要对对权限进行设置，详见 [Graph Explorer](https://developer.microsoft.com/zh-cn/graph/graph-explorer) - 修改权限

#### Graph Explorer

> Microsoft Graph 相关的接口条用集合，类似 postman

[Graph Explorer 地址](https://developer.microsoft.com/zh-cn/graph/graph-explorer)

#### 应用

- [微软代办API](https://docs.microsoft.com/zh-cn/graph/api/resources/todo-overview?view=graph-rest-1.0)