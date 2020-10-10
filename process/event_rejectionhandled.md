<!-- YAML
added: v1.4.1
-->

* `promise` {Promise} 最近处理的 Promise。

每当 `Promise` 被拒绝并且错误处理函数附加到它（例如，使用 [`promise.catch()`]）晚于一个 Node.js 事件循环时，就会触发 `'rejectionHandled'` 事件。

`Promise` 对象之前已经在 `'unhandledRejection'` 事件中触发，但在处理过程中获得了拒绝处理函数。

`Promise` 链中没有顶层的概念，总是可以处理拒绝。
本质上自身是异步的，可以在未来的某个时间点处理 `Promise` 拒绝，可能比触发 `'unhandledRejection'` 事件所需的事件循环更晚。

另一种表述的方式就是，与同步代码中不断增长的未处理异常列表不同，使用 Promise 可能会有一个不断增长和缩小的未处理拒绝列表。

在同步代码中，当未处理的异常列表增长时，会触发 `'uncaughtException'` 事件。

在异步代码中，当未处理的拒绝列表增长时会触发 `'unhandledRejection'` 事件，并且当未处理的拒绝列表缩小时会触发 `'rejectionHandled'` 事件。

```js
const unhandledRejections = new Map();
process.on('unhandledRejection', (reason, promise) => {
  unhandledRejections.set(promise, reason);
});
process.on('rejectionHandled', (promise) => {
  unhandledRejections.delete(promise);
});
```

在这个例子中，`unhandledRejections` 的 `Map` 将随着时间的推移而增长和缩小，反映出拒绝开始未处理然后被处理。
可以定期地（这对可能长时间运行的应用程序最好）或进程退出时（这对脚本来说可能是最方便的）在错误日志中记录此类错误。

