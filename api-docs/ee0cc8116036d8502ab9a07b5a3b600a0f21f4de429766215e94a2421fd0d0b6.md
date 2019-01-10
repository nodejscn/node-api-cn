
`completer` 函数会获取用户输入的当前行作为参数，并返回一个包含以下两个条目的数组：

* 一个包含匹配补全输入的数组。
* 用于匹配的子字符串。

例如：`[[substr1, substr2, ...], originalsubstring]`。

```js
function completer(line) {
  const completions = '.help .error .exit .quit .q'.split(' ');
  const hits = completions.filter((c) => c.startsWith(line));
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

