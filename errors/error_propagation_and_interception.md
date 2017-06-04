
<!--type=misc-->

Node.js 支持几种当应用程序运行时发生的错误的冒泡和处理的机制。
如何报告和处理这些错误完全取决于错误的类型和被调用的 API 的风格。

所有 JavaScript 错误都会被作为异常处理，异常会立即产生并使用标准的 JavaScript `throw` 机制抛出一个错误。
这些都是使用 JavaScript 语言提供的 [`try / catch` 语句]处理的。


```js
// 抛出一个 ReferenceError，因为 z 为 undefined
try {
  const m = 1;
  const n = m + z;
} catch (err) {
  // 在这里处理错误。
}
```

JavaScript 的 `throw` 机制的任何使用都会引起异常，异常必须使用 `try / catch` 处理，否则 Node.js 进程会立即退出。

除了少数例外，同步的 API（任何不接受 `callback` 函数的阻塞方法，例如 [`fs.readFileSync`]）会使用 `throw` 报告错误。

异步的 API 中发生的错误可能会以多种方式进行报告：

- 大多数的异步方法都接受一个 `callback` 函数，该函数会接受一个 `Error` 对象传入作为第一个参数。
  如果第一个参数不是 `null` 而是一个 `Error` 实例，则说明发生了错误，应该进行处理。

<!-- eslint-disable no-useless-return -->
  ```js
  const fs = require('fs');
  fs.readFile('一个不存在的文件', (err, data) => {
    if (err) {
      console.error('读取文件出错！', err);
      return;
    }
    // 否则处理数据
  });
  ```
- 当一个异步方法被一个 `EventEmitter` 对象调用时，错误会被分发到对象的 `'error'` 事件上。

  ```js
  const net = require('net');
  const connection = net.connect('localhost');

  // 添加一个 'error' 事件句柄到一个流：
  connection.on('error', (err) => {
    // 如果连接被服务器重置，或无法连接，或发生任何错误，则错误会被发送到这里。 
    console.error(err);
  });

  connection.pipe(process.stdout);
  ```

- Node.js API 中有一小部分普通的异步方法仍可能使用 `throw` 机制抛出异常，且必须使用 `try / catch` 处理。
  这些方法并没有一个完整的列表；请参阅各个方法的文档以确定所需的合适的错误处理机制。

`'error'` 事件机制的使用常见于[基于流]和[基于事件触发器]的 API，它们本身就代表了一系列的异步操作（相对于要么成功要么失败的单一操作）。

对于所有的 `EventEmitter` 对象，如果没有提供一个 `'error'` 事件句柄，则错误会被抛出，并造成 Node.js 进程报告一个未处理的异常且随即崩溃，除非：
适当地使用 [`domain`] 模块或已经注册了一个 [`process.on('uncaughtException')`] 事件的句柄。

```js
const EventEmitter = require('events');
const ee = new EventEmitter();

setImmediate(() => {
  // 这会使进程崩溃，因为还为添加 'error' 事件句柄。
  ee.emit('error', new Error('这会崩溃'));
});
```

这种方式产生的错误无法使用 `try / catch` 截获，因为它们是在调用的代码已经退出后抛出的。

开发者必须查阅各个方法的文档以明确在错误发生时这些方法是如何冒泡的。

