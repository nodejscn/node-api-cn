<!-- YAML
added: v12.12.0
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `encoding` {string|null} **默认值:** `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `dir` {fs.Dir}

异步地打开目录。 
参阅 opendir(3)。

创建一个 [`fs.Dir`]，其中包含所有用于更进一步读取和清理目录的的函数。

`encoding` 选项用于在打开目录和后续的读取操作时设置 `path` 的字符编码。

