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

如果在事件循环的一次轮询中，一个`Promise`被rejected，并且此`Promise`没有绑定错误处理器，`'unhandledRejection`事件会被触发。
当使用Promises进行编程时，异常会以"rejected promises"的形式封装。Rejections可以被[`promise.catch()`][]捕获并处理，并且在`Promise` chain
中传播。`'unhandledRejection`事件在探测和跟踪promises被rejected，并且rejections未被处理的场景中是很有用的。

此事件监听器的回调函数被传递如下参数:

* `reason` {Error|any} 此对象包含了promise被rejected的相关信息
  (典型情况下，是一个 [`Error`][] 对象).
* `p` 被rejected的promise对象

例如:

```js
process.on('unhandledRejection', (reason, p) => {
  console.log('Unhandled Rejection at:', p, 'reason:', reason);
  // application specific logging, throwing an error, or other logic here
});

somePromise.then((res) => {
  return reportToUser(JSON.pasre(res)); // note the typo (`pasre`)
}); // no `.catch` or `.then`
```

如下代码也会触发`'unhandledRejection'`事件

```js
function SomeResource() {
  // Initially set the loaded status to a rejected promise
  this.loaded = Promise.reject(new Error('Resource not yet loaded!'));
}

const resource = new SomeResource();
// no .catch or .then on resource.loaded for at least a turn
```

在例子中，可以像在其他`'unhandledRejection'`事件的典型场景中一样，跟踪开发者错误导致的rejection。
为了解决这样的错误，`resource.loaded`中可以加一个不做任何操作的[`.catch(() => { })`][`promise.catch()`]处理器，
这样可以阻止`'unhandledRejection'`事件的触发。或者也可以使用[`'rejectionHandled'`][]事件来解决。

