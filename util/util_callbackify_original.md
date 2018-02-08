<!-- YAML
added: v8.2.0
-->

* `original` {Function}  `async` 异步函数
* Returns: {Function} 传统回调函数

将 `async` 异步函数(或者一个返回值为 Promise 的函数)转换成遵循 Node.js 回调风格的函数. 在回调函数中, 第一个参数 err 为 Promise rejected 的原因 (如果 Promise 状态为 resolved , err为 `null` ),第二个参数则是 Promise 状态为 resolved 时的返回值.

例如 :

```js
const util = require('util');

async function fn() {
  return await Promise.resolve('hello world');
}
const callbackFunction = util.callbackify(fn);

callbackFunction((err, ret) => {
  if (err) throw err;
  console.log(ret);
});
```

将会打印出:

```txt
hello world
```

**注意**:

* 回调函数是异步执行的, 并且有异常堆栈错误追踪. 
如果回调函数抛出一个异常, 进程会触发一个 [`'uncaughtException'`][] 异常, 如果没有被捕获, 进程将会退出.

* `null` 在回调函数中作为一个参数有其特殊的意义, 如果回调函数的首个参数为 Promise rejected 的原因且带有返回值, 且值可以转换成布尔值 `false`, 这个值会被封装在 `Error` 对象里, 可以通过属性 `reason` 获取.
  ```js
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && err.hasOwnProperty('reason') && err.reason === null;  // true
  });
  ```

