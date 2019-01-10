<!-- YAML
added: v0.3.4
-->

* `...paths` {string} 路径或路径片段。
* 返回: {string}

将路径或路径片段处理成绝对路径。

`path` 从右到左依次处理，直到构造出绝对路径。
例如，指定的路径片段是：`/foo`、`/bar`、`baz`，则调用 `path.resolve('/foo', '/bar', 'baz')` 会返回 `/bar/baz`。

如果处理完全部 `path` 片段后还未产生绝对路径，则加上当前工作目录。

生成的路径会进行规范化，并且删除末尾的斜杠，除非路径是根目录。

空字符串的 `path` 片段会被忽略。

如果没有指定 `path`，则返回当前工作目录的绝对路径。

```js
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

