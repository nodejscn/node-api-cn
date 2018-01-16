<!-- YAML
added: v0.1.23
-->

* `path` {string}
* 返回: {string}

`path.normalize()` 方法会规范化给定的 `path`，并解析 `'..'` 和 `'.'` 片段。

当发现多个连续的路径分隔符时（如 POSIX 上的 `/` 与 Windows 上的 `\` 或 `/`），它们会被单个的路径分隔符（POSIX 上是 `/`，Windows 上是 `\`）替换。
末尾的多个分隔符会被保留。

如果 `path` 是一个长度为零的字符串，则返回 `'.'`，表示当前工作目录。

例如，在 POSIX 上：

```js
path.normalize('/foo/bar//baz/asdf/quux/..');
// 返回: '/foo/bar/baz/asdf'
```

在 Windows 上：

```js
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// 返回: 'C:\\temp\\foo\\'
```

尽管Windows会识别多种文件路径分隔符，但是两种分隔符在Window上会被(`\`)分隔符取代：

```js
path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// Returns: 'C:\\temp\\foo\\bar'
```

如果 `path` 不是一个字符串，则抛出 [`TypeError`]。

