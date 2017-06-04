<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* 返回: {string}

`path.extname()` 方法返回 `path` 的扩展名，即从 `path` 的最后一部分中的最后一个 `.`（句号）字符到字符串结束。
如果 `path` 的最后一部分没有 `.` 或 `path` 的文件名（见 `path.basename()`）的第一个字符是 `.`，则返回一个空字符串。

例子：

```js
path.extname('index.html');
// 返回: '.html'

path.extname('index.coffee.md');
// 返回: '.md'

path.extname('index.');
// 返回: '.'

path.extname('index');
// 返回: ''

path.extname('.index');
// 返回: ''
```

如果 `path` 不是一个字符串，则抛出 [`TypeError`]。

