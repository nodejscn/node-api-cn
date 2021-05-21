
<!--introduced_in=v0.9.12-->

> 稳定性: 2 - 稳定的

<!-- type=misc -->

Node.js 包含了一个进程外的调试实用程序，可通过 [V8 检查器][V8 Inspector]或内置的调试客户端访问。
要使用它，请使用 `inspect` 参数启动 Node.js，并带上要调试的脚本的路径。
如果出现提示符，则表明调试器已成功启动：

```console
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

Node.js 的调试器客户端不是一个具有全部特性的调试器，但可以进行简单的单步执行和调试。

把 `debugger;` 语句插入到脚本的源代码，则将会在代码中的该位置启用一个断点：


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

一旦执行调试器，则将会在第 3 行出现一个断点：

```console
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

`repl` 命令允许远程地运行代码。
`next` 命令会单步进入下一行。
键入 `help` 可以查看其他可用的命令。

在不键入命令的情况下按 `enter` 键，则会重复上一个调试器命令。

