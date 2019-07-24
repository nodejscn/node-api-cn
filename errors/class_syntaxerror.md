
`Error` 的一个子类，表明程序不是有效的 JavaScript 代码。
这些错误是代码执行的结果产生和传播的。
代码执行可能产生自 `eval`、`Function`、`require` 或 [vm]。
这些错误几乎都表明程序已损坏。


```js
try {
  require('vm').runInThisContext('binary ! isNotOk');
} catch (err) {
  // err 是一个 SyntaxError
}
```

`SyntaxError` 实例在创建它们的上下文中是不可恢复的。
它们只可被其他上下文捕获。

