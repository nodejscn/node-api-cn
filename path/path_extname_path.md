<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: 现在将非字符串作为 `path` 参数传入会抛出异常。
-->

* `path` {string}
* 返回: {string}

`path.extname()` 方法返回 `path` 的扩展名，从最后一次出现 `.`（句点）字符到 `path` 最后一部分的字符串结束。 
如果在 `path` 的最后一部分中没有 `.` ，或者如果 `path` 的基本名称（参阅 `path.basename()`）除了第一个字符以外没有 `.`，则返回空字符串。

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

path.extname('.index.md');
// 返回: '.md'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

