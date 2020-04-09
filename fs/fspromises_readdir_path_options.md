<!-- YAML
added: v10.0.0
changes:
  - version: v10.11.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: New option `withFileTypes` was added.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
  * `withFileTypes` {boolean} **默认值:** `false`。
* 返回: {Promise}

读取目录的内容，然后解决 `Promise` 并带上一个数组（包含目录中的文件的名称，但不包括 `'.'` 和 `'..'`）。

可选的 `options` 参数可以是指定编码的字符串，也可以是具有 `encoding` 属性的对象，该属性指定用于文件名的字符编码。 
如果 `encoding` 设置为 `'buffer'`，则返回的文件名是 `Buffer` 对象。

如果 `options.withFileTypes` 设置为 `true`，则解决的数组将包含 [`fs.Dirent`] 对象。

```js
const fs = require('fs');

async function print(path) {
  const files = await fs.promises.readdir(path);
  for (const file of files) {
    console.log(file);
  }
}
print('./').catch(console.error);
```

