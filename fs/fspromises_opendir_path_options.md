<!-- YAML
added: v12.12.0
changes:
  - version: v13.1.0
    pr-url: https://github.com/nodejs/node/pull/30114
    description: The `bufferSize` option was introduced.
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `bufferSize` {number} 当从目录读取时在内部缓冲的目录条目数。值越高，则性能越好，但内存占用更高。**默认值:** `32`。
* 返回: {Promise} 包含 {fs.Dir}。

异步地打开目录。 
参阅 opendir(3)。

创建一个 [`fs.Dir`]，其中包含所有用于更进一步读取和清理目录的函数。

`encoding` 选项用于在打开目录和后续的读取操作时设置 `path` 的字符编码。

使用异步迭代的示例：

```js
const fs = require('fs');

async function print(path) {
  const dir = await fs.promises.opendir(path);
  for await (const dirent of dir) {
    console.log(dirent.name);
  }
}
print('./').catch(console.error);
```

