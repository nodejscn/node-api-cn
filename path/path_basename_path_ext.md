<!-- YAML
added: v0.1.25
-->

* `path` {String}
* `ext` {String} 可选的文件扩展名
* 返回: {String}

`path.basename()` 方法返回一个 `path` 的最后一部分，类似于 Unix 中的 `basename` 命令。

例子：

```js
path.basename('/foo/bar/baz/asdf/quux.html')
// 返回: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html')
// 返回: 'quux'
```

如果 `path` 不是一个字符串或提供了 `ext` 但不是一个字符串，则抛出 [`TypeError`]。

