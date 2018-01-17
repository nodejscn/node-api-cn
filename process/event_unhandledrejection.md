<!-- YAML
added: v1.4.1
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8217
    description: Not handling Promise rejections has been deprecated.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8223
    description: Unhandled Promise rejections have been will now emit
                 a process warning.
-->

如果在事件循环的一次轮询中，一个 `Promise` 被 rejected，并且此 `Promise` 没有绑定错误处理器，`'unhandledRejection` 事件会被触发。
当使用 Promise 进行编程时，异常会以 "rejected promises" 的形式封装。Rejection 可以被 [`promise.catch()`] 捕获并处理，并且在 `Promise` 链中传播。`'unhandledRejection` 事件在探测和跟踪 promise 被 rejected，并且 rejection 未被处理的场景中是很有用的。

此事件监听器的回调函数被传递如下参数:

* `reason` {Error|any} 此对象包含了 promise 被 rejected 的相关信息（通常是一个 [`Error`] 对象）。
* `p` 被 rejected 的 promise 对象。

例如:

```js
process.on('unhandledRejection', (reason, p) => {
  console.log('未处理的 rejection：', p, '原因：', reason);
  // 记录日志、抛出错误、或其他逻辑。
});

somePromise.then((res) => {
  return reportToUser(JSON.pasre(res)); // 故意输错 `pasre`。
}); // 没有 `.catch` 或 `.then`。
```

如下代码也会触发`'unhandledRejection'`事件

```js
function SomeResource() {
  // 将 loaded 的状态设置为一个 rejected promise。
  this.loaded = Promise.reject(new Error('错误信息'));
}

const resource = new SomeResource();
// resource.loaded 上没有 .catch 或 .then。
```

在例子中，可以像在其他 `'unhandledRejection'` 事件的典型场景中一样，跟踪开发者错误导致的 rejection。
为了解决这样的错误，`resource.loaded` 中可以加一个不做任何操作的 [`.catch(() => { })`][`promise.catch()`] 处理器，
这样可以阻止 `'unhandledRejection'` 事件的触发。或者也可以使用 [`'rejectionHandled'`] 事件来解决。

