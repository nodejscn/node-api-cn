
<!--introduced_in=v0.9.12-->

> 稳定性: 2 - 稳定

<!-- type=misc -->

Node.js 包括一个进程外的调试实用程序，可通过[V8检查器][V8 Inspector]和内置调试客户端访问。
要使用它，请使用 `inspect` 参数启动 Node.js，然后使用要调试的脚本的路径。
将显示一个提示，表明调试器成功启动：

```txt
$ node inspect myscript.js
< Debugger listening on ws://127.0.0.1:9229/80e7a814-7cd3-49fb-921a-2e02228cd5ba
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in myscript.js:1
> 1 (function (exports, require, module, __filename, __dirname) { global.x = 5;
  2 setTimeout(() => {
  3   console.log('world');
debug>
```

Node.js 的调试器客户端不是一个功能齐全的调试器，但可以进行简单的步骤和检查。

将 `debugger;` 语句插入到脚本的源代码，将在代码中的该位置启用断点：


<!-- eslint-disable no-debugger -->
```js
// myscript.js
global.x = 5;
setTimeout(() => {
  debugger;
  console.log('世界');
}, 1000);
console.log('你好');
```

运行调试器后，第 3 行将出现断点：

```txt
$ node inspect myscript.js
< Debugger listening on ws://127.0.0.1:9229/80e7a814-7cd3-49fb-921a-2e02228cd5ba
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in myscript.js:1
> 1 (function (exports, require, module, __filename, __dirname) { global.x = 5;
  2 setTimeout(() => {
  3   debugger;
debug> cont
< 你好
break in myscript.js:3
  1 (function (exports, require, module, __filename, __dirname) { global.x = 5;
  2 setTimeout(() => {
> 3   debugger;
  4   console.log('世界');
  5 }, 1000);
debug> next
break in myscript.js:4
  2 setTimeout(() => {
  3   debugger;
> 4   console.log('世界');
  5 }, 1000);
  6 console.log('你好');
debug> repl
Press Ctrl + C to leave debug repl
> x
5
> 2 + 2
4
debug> next
< 世界
break in myscript.js:5
  3   debugger;
  4   console.log('世界');
> 5 }, 1000);
  6 console.log('你好');
  7
debug> .exit
```

`repl` 命令允许远程运行代码。
`next` 命令将步入下一行。
键入 `help` 以查看可用的其他命令。

在不键入命令的情况下按 `enter` 键将重复上一个调试器命令。

