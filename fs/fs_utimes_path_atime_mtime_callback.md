<!-- YAML
added: v0.4.2
-->

* `path` {String | Buffer}
* `atime` {Integer}
* `mtime` {Integer}
* `callback` {Function}

改变指定的路径所指向的文件的文件时间戳。

注意：`atime` 和 `mtime` 参数遵循以下规则：

- 值应该是一个以秒为单位的 Unix 时间戳。
  例如，`Date.now()` 返回毫秒，所以在传入前应该除以1000。
- 如果值是一个数值字符串，如 `'123456789'`，则该值会被转换为对应的数值。
- 如果值是 `NaN` 或 `Infinity`，则该值会被转换为 `Date.now() / 1000`。

