
* 继承自: {errors.Error}

表明程序不是有效的 JavaScript。
这些错误可能仅在代码评估的结果中产生和传播。 
代码评估可能产生自 `eval`、`Function`、`require` 或 [vm]。
这些错误几乎总是表明程序已损坏。


```js
try {
  require('vm').runInThisContext('nodejs.cn ! 中文网');
} catch (err) {
  // `err` 是一个 SyntaxError。
}
```

`SyntaxError` 实例在创建它们的上下文中是不可恢复的，它们只可能被其他上下文捕获。

