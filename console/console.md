
> 稳定性: 2 - 稳定的

`console` 模块提供了一个简单的调试控制台，它与 Web 浏览器提供的 JavaScript 控制台的机制类似。

该模块导出两个特定组件：

* 一个 `Console` 类，包含 `console.log()` 、 `console.error()` 和 `console.warn()` 等方法，可以用于写入到任何 Node.js 流。
* 一个全局的 `console` 实例，用于写入 [`process.stdout`] 和 [`process.stderr`]。
  全局的 `console` 使用时无需调用 `require('console')`。

注意：全局的 console 对象的方法既不总是同步的（如浏览器中类似的 API），也不总是异步的（如其他 Node.js 流）。
详见 [关于 process I/O]。

例子：使用全局的 `console`：

```js
console.log('hello world');
// 打印: hello world 到 stdout
console.log('hello %s', 'world');
// 打印: hello world 到 stdout
console.error(new Error('错误信息'));
// 打印: [Error: 错误信息] 到 stderr

const name = 'Will Robinson';
console.warn(`Danger ${name}! Danger!`);
// 打印: Danger Will Robinson! Danger! 到 stderr
```

例子：使用 `Console` 类：

```js
const out = getStreamSomehow();
const err = getStreamSomehow();
const myConsole = new console.Console(out, err);

myConsole.log('hello world');
// 打印: hello world 到 out
myConsole.log('hello %s', 'world');
// 打印: hello world 到 out
myConsole.error(new Error('错误信息'));
// 打印: [Error: 错误信息] 到 err

const name = 'Will Robinson';
myConsole.warn(`Danger ${name}! Danger!`);
// 打印: Danger Will Robinson! Danger! 到 err
```

