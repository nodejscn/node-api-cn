
<!--introduced_in=v0.10.13-->

> 稳定性: 2 - 稳定

<!-- source_link=lib/console.js -->

`console` 模块提供了一个简单的调试控制台，类似于 Web 浏览器提供的 JavaScript 控制台。

该模块导出两个特定组件：

* `Console` 类，包含 `console.log()`、`console.error()` 和 `console.warn()` 等方法，可用于写入任何 Node.js 流。
* 全局的 `console` 实例，配置为写入 [`process.stdout`] 和 [`process.stderr`]。
  使用时无需调用 `require('console')`。

注意：全局的 `console` 对象的方法既不像浏览器中的 API 那样总是同步的，也不像其他 Node.js 流那样总是异步的。
详见[进程 I/O][note on process I/O]。

使用全局 `console` 的示例：

```js
console.log('你好世界');
// 打印到 stdout: 你好世界
console.log('你好%s', '世界');
// 打印到 stdout: 你好世界
console.error(new Error('错误信息'));
// 打印错误信息和堆栈跟踪到 stderr：
//   Error: 错误信息
//     at [eval]:5:15
//     at Script.runInThisContext (node:vm:132:18)
//     at Object.runInThisContext (node:vm:309:38)
//     at node:internal/process/execution:77:19
//     at [eval]-wrapper:6:22
//     at evalScript (node:internal/process/execution:76:60)
//     at node:internal/main/eval_string:23:3

const name = '描述';
console.warn(`警告${name}`);
// 打印到 stderr: 警告描述
```

使用 `Console` 类的示例：

```js
const out = getStreamSomehow();
const err = getStreamSomehow();
const myConsole = new console.Console(out, err);

myConsole.log('你好世界');
// 打印到 out: 你好世界
myConsole.log('你好%s', '世界');
// 打印到 out: 你好世界
myConsole.error(new Error('错误信息'));
// 打印到 err: [Error: 错误信息]

const name = '描述';
myConsole.warn(`警告${name}`);
// 打印到 err: 警告描述
```

