<!-- YAML
added: v0.1.13
-->

<!-- type=var -->

* `id` {string} 模块的名称或路径。
* 返回: {any} 导入的模块内容。

用于引入模块、`JSON`、或本地文件。
可以从 `node_modules` 引入模块。
可以使用相对路径（例如 `./`、`./foo`、`./bar/baz`、`../foo`）引入本地模块或 JSON 文件，路径会根据 [`__dirname`] 定义的目录名或当前工作目录进行处理。
POSIX 风格的相对路径会以与操作系统无关的方式解析，这意味着上面的示例将会在 Windows 上以与在 Unix 系统上相同的方式工作。

```js
// 使用相对于 `__dirname` 或当前工作目录的路径引入一个本地模块。
// （在 Windows 上，这会解析为 .\path\myLocalModule。）
const myLocalModule = require('./path/myLocalModule');

// 引入 JSON 文件：
const jsonData = require('./path/filename.json');

// 引入 node_modules 模块或 Node.js 内置模块：
const crypto = require('crypto');
```

