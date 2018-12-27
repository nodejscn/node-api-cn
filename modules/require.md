<!-- YAML
added: v0.1.13
-->

<!-- type=var -->

* {Function}

用于引入模块、JSON 文件、或本地模块。
可以引入 `node_modules` 中的模块。
使用相对路径（比如 `./`、`./foo`、`./bar/baz`、`../foo`）引入本地模块或 JSON 文件时，会根据 [`__dirname`] 定义的目录名或当前工作目录进行处理。

```js
// 引入本地模块：
const myLocalModule = require('./path/myLocalModule');

// 引入 JSON 文件：
const jsonData = require('./path/filename.json');

// 引入 node_modules 中的模块或 Node.js 内置的模块：
const crypto = require('crypto');
```

