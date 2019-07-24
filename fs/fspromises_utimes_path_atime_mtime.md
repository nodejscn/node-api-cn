<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* 返回: {Promise}

更改 `path` 指向的对象的文件系统时间戳，然后在成功时解决 `Promise` 且不带参数。

`atime` 和 `mtime` 参数遵循以下规则：
- 值可以是表示 Unix 纪元时间的数字、`Date` 对象、或类似 `'123456789.0'` 的数值字符串。
- 如果该值无法转换为数值、或值为 `NaN`、`Infinity` 或 `-Infinity`，则抛出 `Error`。

