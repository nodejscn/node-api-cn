
<!--introduced_in=v0.10.13-->

> 稳定性: 2 - 稳定

`console` 模块提供了一个调试控制台，类似于 Web 浏览器提供的 JavaScript 控制台。

该模块有两个组件：

* `Console` 类，包含 `console.log()`、`console.error()` 和 `console.warn()` 等方法，可用于写入到任何 Node.js 流。
* 全局的 `console` 实例，可用于写入到 [`process.stdout`] 和 [`process.stderr`]。
  使用时无需调用 `require('console')`。

全局的 `console` 对象的方法既不像浏览器中的 API 那样总是同步的，也不像其他 Node.js 流那样总是异步的。
详见 [进程 I/O][note on process I/O]。

例子，使用全局的 `console`：

```js
console.log('你好世界');
// 输出 '你好世界' 到 stdout。
console.log('你好%s', '世界');
// 输出 '你好世界' 到 stdout。
console.error(new Error('错误信息'));
// 输出 '[Error: 错误信息]' 到 stderr。

const name = '描述';
console.warn(`警告${name}`);
// 输出 '警告描述' 到 stderr。
```

例子，使用 `Console` 类：

```js
const out = getStreamSomehow();
const err = getStreamSomehow();
const myConsole = new console.Console(out, err);

myConsole.log('你好世界');
// 输出 '你好世界' 到 out。
myConsole.log('你好%s', '世界');
// 输出 '你好世界' 到 out。
myConsole.error(new Error('错误信息'));
// 输出 '[Error: 错误信息]' 到 err。

const name = '描述';
myConsole.warn(`警告${name}`);
// 输出 '警告描述' 到 err。
```

