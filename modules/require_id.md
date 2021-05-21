<!-- YAML
added: v0.1.13
-->

<!-- type=var -->

* `id` {string} 模块名称或者路径。
* 返回: {any} 导出的模块内容。

被用于导入模块、`JSON`、以及本地的文件。
模块可以被从 `node_modules` 导入。
本地的模块和 JSON 文件可以被使用一个相对的路径（例如 `./`、`./foo`、`./bar/baz`、`../foo`）导入，这会被根据由 [`__dirname`]（如果已定义）指定的目录或者当前工作目录进行解析。
POSIX 风格的相对路径会被以一种与操作系统无关的方式解析，这意味着上面的示例在 Windows 上会以与它们在 Unix 系统上相同的方式工作。

```js
// 使用一个相对于 `__dirname` 或当前工作目录的路径导入一个本地的模块。
// （在 Windows 上，这会解析为 .\path\myLocalModule。）
const myLocalModule = require('./path/myLocalModule');

// 导入一个 JSON 文件：
const jsonData = require('./path/filename.json');

// 导入一个来自 node_modules 的模块或者 Node.js 内置的模块：
const crypto = require('crypto');
```

