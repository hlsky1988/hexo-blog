---
title: pc 移动端 切换处理
tags:
  - H5
  - PC
  - 切换
originContent: ''
categories:
  - 记录
toc: false
date: 2021-02-20 17:36:15
---

- pc端地址 http://xxx.com/xxx
- 移动端地址 http://xxx.com/m/xxx

```javascript
function isMobileAccess() {
var sUserAgent = navigator.userAgent;
var mobileAgents = ['iPad', 'iPhone', 'iPod', 'Android', 'android'];
for (var i = 0, len = mobileAgents.length; i < len; i++) {
if (sUserAgent.indexOf(mobileAgents[i]) !== -1) {
return true;
}
}
return false;
}
var protocol = location.protocol;
var host = location.host;
var pathname = location.pathname;
var href;

console.log('当前移动端访问       '+isMobileAccess())

if (isMobileAccess()&&!/\/m/.test(pathname)) {
href = protocol+'//'+host+'/m'+pathname
}else if(!isMobileAccess()&&/\/m/.test(pathname)){
pathname = pathname.replace(/\/m/,'')
href = protocol+'//'+host+pathname
}

if (href) {
location.href = href
}

```

```

