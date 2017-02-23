<!-- YAML
added: v0.1.16
-->

* `path` {String}
* 返回: {String}

`path.dirname()` 方法返回一个 `path` 的目录名，类似于 Unix 中的 `dirname` 命令。

例子：

```js
path.dirname('/foo/bar/baz/asdf/quux')
// 返回: '/foo/bar/baz/asdf'
```

如果 `path` 不是一个字符串，则抛出 [`TypeError`]。

