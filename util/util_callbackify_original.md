<!-- YAML
added: v8.2.0
-->

* `original` {Function}  `async` 异步函数。
* 返回: {Function} 传统回调函数。

将 `async` 异步函数（或者一个返回值为 `Promise` 的函数）转换成遵循异常优先的回调风格的函数，例如将 `(err, value) => ...` 回调作为最后一个参数。
在回调函数中，第一个参数为拒绝的原因（如果 `Promise` 解决，则为 `null`），第二个参数则是解决的值。

```js
const util = require('util');

async function fn() {
  return 'hello world';
}
const callbackFunction = util.callbackify(fn);

callbackFunction((err, ret) => {
  if (err) throw err;
  console.log(ret);
});
```

将会打印出：

```text
hello world
```

回调函数是异步执行的，并且有异常堆栈错误追踪。
如果回调函数抛出一个异常，进程会触发一个 [`'uncaughtException'`][] 异常，如果没有被捕获，进程将会退出。

`null` 在回调函数中作为一个参数有其特殊的意义，如果回调函数的首个参数为 `Promise` 拒绝的原因且带有返回值，且值可以转换成布尔值 `false`，这个值会被封装在 `Error` 对象里，可以通过属性 `reason` 获取。

```js
function fn() {
  return Promise.reject(null);
}
const callbackFunction = util.callbackify(fn);

callbackFunction((err, ret) => {
  // 当 Promise 被以 `null` 拒绝时，它被包装为 Error 并且原始值存储在 `reason` 中。
  err && err.hasOwnProperty('reason') && err.reason === null;  // true
});
```

