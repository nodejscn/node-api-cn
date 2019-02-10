<!-- YAML
added: v0.1.23
-->

* `path` {string}
* 返回: {string}

`path.normalize()` 方法规范化给定的 `path`，解析 `'..'` 和 `'.'` 片段。

当找到多个连续的路径段分隔字符时（例如 POSIX 上的 `/`、Windows 上的 `\` 或 `/`），则它们将被替换为单个平台特定的路径段分隔符（POSIX 上的 `/`、Windows 上的 `\`）。 
尾部的分隔符会保留。

如果 `path` 是零长度的字符串，则返回 `'.'`，表示当前工作目录。

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

由于 Windows 识别多种路径分隔符，因此这些分隔符都将被替换为 Windows 首选的分隔符（`\`）：

```js
path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// 返回: 'C:\\temp\\foo\\bar'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

