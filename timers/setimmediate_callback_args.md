<!-- YAML
added: v0.9.1
-->

* `callback` {Function} Node.js [事件循环][Event Loop]的此回合结束时要调用的函数。
* `...args` {any} 当调用 `callback` 时传入的可选的参数。
* 返回: {Immediate} 用于 [`clearImmediate()`]。

安排在 I/O 事件的回调之后立即执行的 `callback`。

当多次调用 `setImmediate()` 时，`callback` 函数会按它们被创建的顺序放入排队等待执行。
每轮的事件循环迭代都会处理整个回调队列。
如果一个 immediate 定时器是从一个正在执行中的回调内部被放入队列，则该定时器将不会被触发，直到下一轮的事件循环迭代。

如果 `callback` 不是函数，则抛出 [`TypeError`]。

此方法有一个定制的用于 promise 的变体，使用 [`util.promisify()`] 创建：

```js
const util = require('util');
const setImmediatePromise = util.promisify(setImmediate);

setImmediatePromise('foobar').then((value) => {
  // value === 'foobar' （传值是可选的）
  // 这会在所有的 I/O 回调之后执行。
});

// 或使用异步函数。
async function timerExample() {
  console.log('在 I/O 回调之前');
  await setImmediatePromise();
  console.log('在 I/O 回调之后');
}
timerExample();
```

