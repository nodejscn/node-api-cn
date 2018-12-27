<!-- YAML
added: v0.1.23
-->

* `path` {string}
* 返回: {string}

规范化 `path`，并处理 `'..'` 和 `'.'` 片段。

如果出现多个连续的路径分隔符（如 POSIX 上的 `/` 或 Windows 上的 `\` 与 `/`），则替换为单个分隔符。
末尾的多个分隔符会被保留。

如果 `path` 是空字符串，则返回 `'.'`，表示当前工作目录。

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

如果 Windows 上出现多种路径分隔符，则都使用 `\` 替换：

```js
path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// 返回: 'C:\\temp\\foo\\bar'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

