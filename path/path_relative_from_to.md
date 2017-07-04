<!-- YAML
added: v0.5.0
changes:
  - version: v6.8.0
    pr-url: https://github.com/nodejs/node/pull/8523
    description: On Windows, the leading slashes for UNC paths are now included
                 in the return value.
-->

* `from` {string}
* `to` {string}
* 返回: {string}

`path.relative()` 方法返回从 `from` 到 `to` 的相对路径（基于当前工作目录）。
如果 `from` 和 `to` 各自解析到同一路径（调用 `path.resolve()`），则返回一个长度为零的字符串。

如果 `from` 或 `to` 传入了一个长度为零的字符串，则当前工作目录会被用于代替长度为零的字符串。

例如，在 POSIX 上：

```js
path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
// 返回: '../../impl/bbb'
```

在 Windows 上：

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb');
// 返回: '..\\..\\impl\\bbb'
```

如果 `from` 或 `to` 不是一个字符串，则抛出 [`TypeError`]。

