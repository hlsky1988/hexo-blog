---
title: node server端一些有用的库
tags:
  - node
  - server
categories:
  - 记录
toc: true
date: 2021-02-20 17:10:23
---

# 使用前的准备工作

## n

- 用来升级node版本,不支持Windows,
- 一般用 n lts 来跟随 node lts版本

## nvm

- node版本切换工具

## nrm/yrm

- node/yarn 源管理切换工具

## mirror-config-china

- 为中国内地的Node.js开发者准备的镜像配置，大大提高node模块安装速度。
- 自动配置各个node模块的安装源为淘宝镜像

## 脚本内安装出现错误的处理

- node-sass/Puppeteer/Windows-build-tools之类的通过安装脚本来安装的工具,会因为脚本内源地址的问题安装失败
- 此时使用cnpm安装有奇效
- cnpm 将脚本内的源地址替换为国内源
- 需要注意使用cnpm可能会导致webstorm崩溃的问题

# 未分类

## nodemon

- [npm](https://www.npmjs.com/package/nodemon)
- nodemon用来监视node.js应用程序中的任何更改并自动重启服务,非常适合用在开发环境中。

## consola

- [npm](https://www.npmjs.com/package/consola)
- 色彩鲜明的 console 输出，明显的提示作用
- 注意文档未说明的 ready 效果

```javascript
consola.ready({
  message: `Server running at : \n- Local   : http://localhost:${part}\n- Network : http://${ip}:${part}`,
  badge:true
});
```

## Chalk 彩色终端输出

- npm: https://www.npmjs.com/package/chalk
- 彩色终端输出

## ora 终端在执行长时间任务时的状态变化提醒

- npm: https://www.npmjs.com/package/ora
- 终端在执行长时间任务时的状态变化提醒

## enquirer & inquirer

- [npm](https://www.npmjs.com/package/enquirer)
- Stylish CLI prompts that are user-friendly, intuitive and easy to create.
- node-server-side 输入交互

## concurrently

- Run multiple commands concurrently. Like npm run watch-js & npm run watch-less but better.

## Node Schedule & node-cron

- 在node中定时执行某些任务

## request-ip

- [npm-link](https://www.npmjs.com/package/request-ip)
- 用于获取请求的ip地址

## geoip-lite

- [npm-link](https://www.npmjs.com/package/geoip-lite)
- 根据IP获取位置信息

## shelljs

- 在node中运行shell

## shell.js

- 创建网页HTML终端

## ioredis

- node 端 Redis 操作库
- npm地址: https://www.npmjs.com/package/ioredis

## NeDB

- JavaScript内存/文件数据库
- npm地址: https://www.npmjs.com/package/nedb#bug-reporting-guidelines
- 其 API 是 MongoDB 的一个子集 , 详情见[快速上手](http://www.alloyteam.com/2016/03/node-embedded-database-nedb/)

## PoloDB

- 一个非常轻量级的 NoSQL 数据库，有着类似 MongoDB 的 API
- https://v2ex.com/t/727979#reply36
- npm地址: https://www.npmjs.com/package/polodb
- repo: https://github.com/vincentdchan/PoloDB

## get-port

- npm: https://www.npmjs.com/package/get-port
- 获取一下可能的端口

## address

- npm: https://www.npmjs.com/package/address
- 获取当前网络信息 IP、Mac、IPv6 等

## public-ip

- npm 懒得贴了
- 获取当前公网地址

## wordcloud2.js

- 官网: https://wordcloud2-js.timdream.org/#love
- npm: https://www.npmjs.com/package/wordcloud
- 词云的js生成库(canvas/element)

# node脚手架项目 自动格式化

## Husky

- npm: https://www.npmjs.com/package/husky
- 中文文档: http://docs.breword.com/typicode-husky/
- 结合 https://prettier.io/ 在各编辑器的插件

> .prettierrc

```
{
  "trailingComma": "es5",
  "indent_style": "space",
  "indent_size": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "end-of-line": "lf"
}
```

# node脚本 参数相关

## cross-env

- 用于设置 node 端多环境环境变量
- 以下代码截取自某 package.json

```JSON {.line-numbers}
"scripts": {
    "dev": "cross-env NODE_ENV=development nodemon server/index.js --watch server",
    "build": "nuxt build",
    "start": "cross-env NODE_ENV=production node server/index.js",
    "generate": "nuxt generate"
}
```

- 通过 process.env.NODE_ENV 获取变量

## nconf

- 同cross-env, node端生成、读取、修改启动参数 [npm_link](https://www.npmjs.com/package/nconf#nconfusename-options)

```javascript
var fs = require('fs'),
  nconf = require('nconf');

//
// Setup nconf to use (in-order):
//   1. Command-line arguments
//   2. Environment variables
//   3. A file located at 'path/to/config.json'
//
nconf.argv()
  .env()
  .file({ file: './config.json' });

//
// Set a few variables on `nconf`.
//
nconf.set('database:host', '127.0.0.1');
nconf.set('database:port', 5984);
nconf.set('user', 'root');

//
// Get the entire database object from nconf. This will output
// { host: '127.0.0.1', port: 5984 }
//
console.log('foo: ' + nconf.get('foo'));
console.log('NODE_ENV: ' + nconf.get('NODE_ENV'));
console.log('database: ' + JSON.stringify(nconf.get('database')));
console.log('database:host ' + nconf.get('database').host);
console.log('user: ' + nconf.get('user'));

//
// Save the configuration object to disk
//
nconf.save(function (err) {
  fs.readFile('./config.json', function (err, data) {
    console.log(JSON.parse(data.toString()))
  });
  // console.log(require('./config.json'));
});
```

> 运行结果 `node ./nconf.js --NODE_ENV=production --foo bar`

```
foo: bar
NODE_ENV: production
database: {"host":"127.0.0.1","port":5984}
database:host 127.0.0.1
user: root
{ database: { host: '127.0.0.1', port: 5984 }, user: 'root' }
```

## commander

- node.js 命令行接口的完整解决方案
- npm: https://www.npmjs.com/package/commander
- 中文文档: https://github.com/tj/commander.js/blob/HEAD/Readme_zh-CN.md

# headless浏览器、爬虫

## PhantomJS

- 可脚本化无头浏览器
- PhantomJS是一款无脚网页浏览器，支持JavaScript脚本。它运行在Windows，macOS，Linux和FreeBSD上。使用QtWebKit作为后端，它为各种Web标准提供了快速和本地支持：DOM处理，CSS选择器，JSON，Canvas和SVG。
- PhantomJS的以下简单脚本加载Google主页，稍等片刻，然后将其捕获到图像。

```javascript
var page = require('webpage').create();
page.open('http://www.google.com', function() {
    setTimeout(function() {
        page.render('google.png');
        phantom.exit();
    }, 200);
});
```

- 坑多,目前停止更新

## Puppeteer

- 谷歌推出的 headless Chrome 项目
- 持续更新中
- PhantomJS 能做的它都能做
- PhantomJS 作者因为此项目停止更新
- [NPM地址](https://www.npmjs.com/package/puppeteer)

## cheerio

- Fast, flexible, and lean implementation of core jQuery designed specifically for the server.
- node 端爬虫

# 股票爬虫/数据

## tushare.js

- https://github.com/waditu/tushare.js
- 最后更新 2017年5月26日

## dipiper

- https://github.com/andyesfly/dipiper
- [文档地址](https://dipiper.tech/#/README)

# express 中间件

## express-minify

- npm: https://www.npmjs.com/package/express-minify
- 自动压缩（和缓存）JavaScript、CSS和JSON文件。它还支持以下 sass、less、stylus、CoffeeScript的编译和压缩。
- 建议与 expressjs/compression 中间件一起使用

## compression

- npm： https://www.npmjs.com/package/compression
- 开启Gzip压缩，文本类文件传输体积缩小50%以上

# 图形验证码

> 关于图形验证码: [如何用 Node.js 制作验证码？- 知乎](https://www.zhihu.com/question/32156977)

> 时间线不短, 有的回答都超过5年了,参考一下就好

## node-canvas

- npm: https://www.npmjs.com/package/canvas
- 需要依赖Python和Windows-build-tools
- 相关使用: https://segmentfault.com/a/1190000007528623

## GM

- npm: https://www.npmjs.com/package/gm
- 依赖：
  - brew install imagemagick
  - brew install graphicsmagick

## sharp

- npm: https://www.npmjs.com/package/sharp
- 以性能出众的nodejs端图像处理工具
- 不需要第三方依赖，待验证

## ccap

- npm: https://www.npmjs.com/package/ccap
- node-ccap —— node.js generate captcha using c++ library CImg.
- 由于是C++,所以Windows平台需要Python和Windows-build-tools来编译node-gyp,相关依赖体积不小,需要科学上网
- last commit on Jul 6, 2016

## svg-captcha

- npm: https://www.npmjs.com/package/svg-captcha
- 中文介绍: https://github.com/produck/svg-captcha/blob/HEAD/README_CN.md
- 不需要安装 c++ 模块
- 生成svg比jpg体积小,且更不容易被机器识别
- 当前时间: 2020-05-25 Weekly Downloads 10.4K
- 相关: http://www.ptbird.cn/node-js-svg-captcha.html

## trek-captcha

- npm: https://www.npmjs.com/package/trek-captcha
- A Lightweight Pure JavaScript Captcha for Node.js. No C/C++, No ImageMagick, No canvas. Inspired By rucaptcha.
- last version: 0.4.0
- last commit: 12 Jul 2018

## node-gd-bmp

- npm: https://www.npmjs.com/package/gd-bmp
- 光及高速和100％的js实现图形库，它可以在任何平台上运行，但只支持24位的BMP格式，内部包含3种字体

# npm 私服

## Verdaccio

- https://verdaccio.org/zh-CN/
- https://github.com/verdaccio/verdaccio
- 一个开源轻量的npm私服

# CMS

## nodercms

- 官网：http://www.nodercms.com
- github：https://github.com/welkinwong/nodercms
- express & handlerbar & MongoDB

## DoraCMS

- 官网：www.html-js.cn
- github：https://github.com/doramart/DoraCMS
- eggjs + mongodb + Vue
- 提供 Swagger 生成的文档，观感上较 nodercms 更清晰
- 提供了 my-sql 版本 https://github.com/doramart/DoraCMS-SQL