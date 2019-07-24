<!-- YAML
added: v0.7.9
-->

* {string}

提供平台特定的路径片段分隔符：

* Windows 上是 `\`。
* POSIX 上是 `/`。

例如，在 POSIX 上：

```js
'foo/bar/baz'.split(path.sep);
// 返回: ['foo', 'bar', 'baz']
```

在 Windows 上：

```js
'foo\\bar\\baz'.split(path.sep);
// 返回: ['foo', 'bar', 'baz']
```

在 Windows 上，正斜杠（`/`）和反斜杠（`\`）都被接受为路径片段分隔符。
但是，`path` 方法只添加反斜杠（`\`）。


