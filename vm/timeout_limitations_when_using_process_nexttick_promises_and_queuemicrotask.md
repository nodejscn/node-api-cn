
由于在 V8 和 Node.js 中实现了 `process.nextTick()` 队列和作为 Promise 基础的微任务队列的内部机制，因此在上下文中运行的代码可以使用 `vm.runInContext()`、`vm.runInNewContext()` 和 `vm.runInThisContext()` 转义 `timeout`。


例如，`vm.runInNewContext()` 执行的以下代码（超时为 5 毫秒）会在 promise 解决后调度无限循环。 
调度的循环永远不会被超时中断：

```js
const vm = require('vm');

function loop() {
  while (1) console.log(Date.now());
}

vm.runInNewContext(
  'Promise.resolve().then(loop);',
  { loop, console },
  { timeout: 5 }
);
```

使用 `process.nextTick()` 和 `queueMicrotask()` 函数调度 `loop()` 调用时也会发生此问题。

出现此问题是因为所有上下文共享相同的微任务和 nextTick 队列。

