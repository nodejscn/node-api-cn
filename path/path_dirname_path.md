<!-- YAML
added: v0.1.16
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* 返回: {string}

`path.dirname()` 方法返回一个 `path` 的目录名，类似于 Unix 中的 `dirname` 命令。
Trailing directory separators are ignored, see [`path.sep`][].

例子：

```js
path.dirname('/foo/bar/baz/asdf/quux');
// 返回: '/foo/bar/baz/asdf'
```

如果 `path` 不是一个字符串，则抛出 [`TypeError`]。

