---
title: 批量删除 node_modules
tags:
  - node_modules
  - 批量
  - 删除
originContent: ''
categories:
  - 记录
toc: false
date: 2021-02-20 17:16:46
---

- [npkill](https://www.npmjs.com/package/npkill)

```
npm npkill --dirrectory ~/dev
```

- sh 命令

```
rm -rf $(find ~ -name node_modules -type d)
```

