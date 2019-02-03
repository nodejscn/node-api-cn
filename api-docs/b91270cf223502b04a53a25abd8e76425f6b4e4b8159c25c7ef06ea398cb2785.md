<!-- YAML
added: v10.12.0
-->

* `type` {string} 错误类型。`'resolve'` 或 `'reject'` 之一。
* `promise` {Promise} 不止一次解决或拒绝的 Promise。
* `value` {any} 在原始解析后解决或拒绝的 Promise 的值。

只要 `Promise` 有以下情况，就会触发 `'multipleResolves'` 事件：

* 解决不止一次。
* 拒绝不止一次。
* 解决后拒绝。
* 拒绝后解决。

这对于在使用 Promise 构造函数时跟踪应用程序中的错误很有用。
否则，由于处于死区，这些错误会被默默地吞没。

建议结束此类错误的进程，因为该进程可能处于未定义状态。
使用 Promise 构造函数时，请确保每次调用时确保触发 `resolve()` 或 `reject()` 函数，并且永远不会在同一个调用中同时调用这两个函数。

```js
process.on('multipleResolves', (type, promise, reason) => {
  console.error(type, promise, reason);
  setImmediate(() => process.exit(1));
});

async function main() {
  try {
    return await new Promise((resolve, reject) => {
      resolve('第一次调用');
      resolve('吞没解决');
      reject(new Error('吞没解决'));
    });
  } catch {
    throw new Error('失败');
  }
}

main().then(console.log);
// resolve: Promise { '第一次调用' } '吞没解决'
// reject: Promise { '第一次调用' } Error: 吞没解决
//     at Promise (*)
//     at new Promise (<anonymous>)
//     at main (*)
// 第一次调用
```

