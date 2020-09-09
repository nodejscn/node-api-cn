<!-- YAML
added:
 - v11.4.0
 - v10.16.0
changes:
  - version:
     - v11.14.0
     - v10.17.0
    pr-url: https://github.com/nodejs/node/pull/26989
    description: Symbol.asyncIterator support is no longer experimental.
-->

* 返回: {AsyncIterator}

创建一个 `AsyncIterator` 对象，该对象以字符串形式迭代输入流中的每一行。 
这个方法允许 `readline.Interface` 对象使用 `for await...of` 循环的异步迭代。

输入流中的错误不会被转发。

如果循环以 `break`，`throw` 或 `return` 终止，则 [`rl.close()`] 将会被调用。 
换句话说，对 `readline.Interface` 的迭代将会始终完全消费输入流。

性能比不上传统的 `'line'` 事件的 API。 
对于性能敏感的应用程序，请使用 `'line'`。

```js
async function processLineByLine() {
  const rl = readline.createInterface({
    // ...
  });

  for await (const line of rl) {
    // readline 输入中的每一行将会在此处作为 `line`。
  }
}
```

`readline.createInterface()` will start to consume the input stream once
invoked. Having asynchronous operations between interface creation and
asynchronous iteration may result in missed lines.

