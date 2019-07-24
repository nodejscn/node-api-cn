<!-- YAML
added: v0.3.4
-->

* `...paths` {string} 路径或路径片段的序列。
* 返回: {string}

`path.resolve()` 方法将路径或路径片段的序列解析为绝对路径。

给定的路径序列从右到左进行处理，每个后续的 `path` 前置，直到构造出一个绝对路径。
例如，给定的路径片段序列：`/foo`、`/bar`、`baz`，调用 `path.resolve('/foo', '/bar', 'baz')` 将返回 `/bar/baz`。

如果在处理完所有给定的 `path` 片段之后还未生成绝对路径，则再加上当前工作目录。

生成的路径已规范化，并且除非将路径解析为根目录，否则将删除尾部斜杠。

零长度的 `path` 片段会被忽略。

如果没有传入 `path` 片段，则 `path.resolve()` 将返回当前工作目录的绝对路径。

```js
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

如果任何参数不是字符串，则抛出 [`TypeError`]。

