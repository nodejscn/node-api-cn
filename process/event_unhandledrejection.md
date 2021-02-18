<!-- YAML
added: v1.4.1
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8217
    description: 不建议不处理 `Promise` 的拒绝。
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8223
    description: 未处理的 `Promise` 拒绝现在会触发进程警告。
-->

* `reason` {Error|any} Promise 被拒绝的信息（通常是 [`Error`] 对象）。
* `promise` {Promise} 被拒绝的 promise。

当 `Promise` 被拒绝且在事件循环的此次轮询中没有绑定错误句柄时，则会触发 `'unhandledRejection` 事件。
当使用 Promise 进行编程时，异常会被封装为“被拒绝的 promise”。
拒绝可以被 [`promise.catch()`] 捕获并处理，并且在 `Promise` 链中传播。
`'unhandledRejection` 事件在检测和跟踪被拒绝的（且拒绝还未被处理）promise 时很有用。


```js
process.on('unhandledRejection', (reason, promise) => {
  console.log('未处理的拒绝：', promise, '原因：', reason);
  // 记录日志、抛出错误、或其他逻辑。
});

somePromise.then((res) => {
  return reportToUser(JSON.pasre(res)); // 故意输错 (`pasre`)。
}); // 没有 `.catch()` 或 `.then()`。
```

以下代码也会触发 `'unhandledRejection'` 事件：

```js
function SomeResource() {
  // 设置 loaded 的状态为被拒绝的 promise。
  this.loaded = Promise.reject(new Error('错误信息'));
}

const resource = new SomeResource();
// resource.loaded 上没有 .catch 或 .then。
```

在此示例中，可以像其他 `'unhandledRejection'` 事件一样，将拒绝作为开发者错误进行跟踪。
为了解决此类故障，可以在 `resource.loaded` 上绑定一个无操作的 [`.catch(() => { })`][`promise.catch()`] 句柄，这样就可以阻止 `'unhandledRejection'` 事件的触发。

