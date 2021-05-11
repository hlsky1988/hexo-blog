---
title: 用JavaScript来写系统脚本
tags:
  - node
  - 脚本
  - mjs
originContent: ''
categories:
  - 记录
toc: false
date: 2021-05-11 16:53:50
---

平时写的脚本都是`.sh`或者 Python 脚本，在[v2ex](https://www.v2ex.com/t/776136#r_10514394)上看到有人介绍的这样一个库：

- [zx](https://www.npmjs.com/package/zx)
- npm: https://www.npmjs.com/package/zx
- github: https://github.com/google/zx

看介绍，是对 node `child_process` 的封装, 接下来是对部分文档内容的翻译

1.  安装
    `npm i -g zx`
1.  关于脚本后缀名

    - 建议使用 `.mjs`, 以便在全局使用 `await` 特性
    - 如果更喜欢使用 `.js` 作为脚本后缀名, 则建议将脚本内容写在无返回值的异步函数中 `async function () {...}()`

1.  在脚本的开头添加 shebang
    - `#!/usr/bin/env zx`
    - 什么是 shebang?
      - 即脚本开头 `#!` 和之后的内容,它声明了脚本的解释程序,如缺失,则默认使用 shell 去解释当前脚本
      - 需要使用绝对路径
1.  添加执行权限并运行
    - ```
      chmod +x ./script.mjs
      ./script.mjs
      ```
    - 也可以通过`zx`来运行 `zx ./script.mjs`
      - 添加 shebang 后或者通过`zx`来运行脚本时,不需要引入 `$` `cd` `fetch` 等变量
1.  相关命令

    1.  ```
        $`command`
        ```

        - 通过`child_process.exec`来执行用户命令,返回一个 `Promise<ProcessOutput>`

          - 🌰:

            ```js
            let hosts = [...]
            await Promise.all(hosts.map(host =>
              $`rsync -azP ./src ${host}:/var/www`
            ))

            ```

        - 运行出错时,返回的 `exitCode` 不为 0

          - 🌰:

            ```js
            try {
              await $`exit 1`
            } catch (p) {
              console.log(`Exit code: ${p.exitCode}`)
              console.log(`Error: ${p.stderr}`)
            }
            ```

        - 输出类型

          ```ts
          class ProcessOutput {
            readonly exitCode: number
            readonly stdout: string
            readonly stderr: string
            toString(): string
          }
          ```

    1.  cd

        - ```js
          cd('/tmp')
          await $`pwd` // outputs /tmp
          ```

    1.  fetch

        - 这是 [node-fetch](https://www.npmjs.com/package/node-fetch) 的封装

        - 🌰

          ```js
          let resp = await fetch('http://wttr.in')

          if (resp.ok) {
            console.log(await resp.text())
          }
          ```

    1.  question

        - 这是 [readline](https://nodejs.org/api/readline.html) 的封装

          - ```ts
            type QuestionOptions = { choices: string[] }

            function question(
              query: string,
              options?: QuestionOptions
            ): Promise<string>
            ```

        - 🌰
          ```js
          let username = await question('What is your username? ')
          let token = await question('Choose env variable: ', {
            choices: Object.keys(process.env),
          })
          ```

    1.  [chalk](https://www.npmjs.com/package/chalk)
        - ```js
          console.log(chalk.blue('Hello world!'))
          ```
    1.  fs

        - `fs`可直接使用,不需要`require`或者`import`
        - ```js
          let content = await fs.readFile('./package.json')
          ```
        - 默认导入 Promise 版本,等于以下写法

          ```js
          import { promises as fs } from 'fs'
          ```

    1.  更多内容详见 npm 或者 GitHub
        - npm: https://www.npmjs.com/package/zx
        - github: https://github.com/google/zx

1.  执行远程脚本

    - 当参数以`https://`开头,则当做远程脚本下载并执行

      ```
      zx https://medv.io/example-script.mjs
      ```

> 记录完毕
