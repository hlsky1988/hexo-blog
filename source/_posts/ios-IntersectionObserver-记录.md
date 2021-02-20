---
title: ios IntersectionObserver 记录
tags:
  - IntersectionObserver
  - ios
originContent: ''
categories:
  - 记录
toc: false
date: 2021-02-20 17:22:27
---

> 日期: 2020.07.18

> 状况描述: iOS iPhone7 12.1.4 safari H5 js 执行异常, iPhone 6s 13.3 正常

排查原因: IntersectionObserver 引起的兼容问题

[查看 IntersectionObserver 兼容情况](https://caniuse.com/#search=IntersectionObserver)

![image](https://p.pstatp.com/origin/137dc00004a46aa68b313)

可以看到, 12.2以下不支持，覆盖机型1.03%

# 查看 iOS 版本分布情况

- 官网数据: https://developer.apple.com/cn/support/app-store/
  - 由 App Store 在 2020 年 6 月 17 日实测而来, 仅iPhone:
  - 92% iOS 13
  - 7% iOS 12
  - 2% 较早版本
  - 说明: 101%这个确实是官网给的数据
- iosversionstats: https://www.david-smith.org/iosversionstats/
  - Last Updated: 2020年1月28日 23:34:27 iPhone Only:
  - 13.X	94.0%
  - 12.X	4.6%
  - 11.X	0.7%
  - 10.X	0.5%
  - 9.X	0.1%

> 都只有大版本的分布,没有小版本的分布情况

# 解决方法

- 尝试 intersection-observer
  - 此插件ie是可以工作的
  - iOS 12.1.4 测试可以工作

