
当被调用时，用户输入的当前行会被提供给 `completer` 函数，并返回一个包含以下两个条目的数组：

* 一个包含匹配补全输入的数组。
* 用于匹配的子字符串。

例如：`[[substr1, substr2, ...], originalsubstring]`。

```js
function completer(line) {
  const completions = '.help .error .exit .quit .q'.split(' ');
  const hits = completions.filter((c) => { return c.indexOf(line) === 0 });
  // 如果没匹配到则展示全部补全
  return [hits.length ? hits : completions, line];
}
```

如果 `completer` 函数接受两个参数，则可被异步地调用：

```js
function completer(linePartial, callback) {
  callback(null, [['123'], linePartial]);
}
```

