
> 稳定性: 2 - 稳定的

<!-- type=misc -->

Node.js 包含一个进程外的调试工具，可以通过一个基于 TCP 协议且内置的调试客户端访问。
要使用它，需要以 `inspect` 参数启动 Node.js，并带上需要调试的脚本的路径；然后会出现一个提示，表明已成功启动调试器：

```txt
$ node inspect myscript.js
< Debugger listening on ws://127.0.0.1:9229/80e7a814-7cd3-49fb-921a-2e02228cd5ba
< For help see https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in myscript.js:1
> 1 (function (exports, require, module, __filename, __dirname) { global.x = 5;
  2 setTimeout(() => {
  3   console.log('world');
debug>
```

Node.js 的调试器客户端还未支持全部特性，但可以做些简单的步骤和检测。

在脚本的源代码中插入 `debugger;` 语句，则会在代码的那个位置启用一个断点：

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

一旦运行调试器，则在第 3 行会出现一个断点：

$ node inspect myscript.js
< Debugger listening on ws://127.0.0.1:9229/80e7a814-7cd3-49fb-921a-2e02228cd5ba
< For help see https://nodejs.org/en/docs/inspector
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
> 2+2
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

`repl` 命令用于运行代码。
`next` 命令用于步入下一行。
输入 `help` 可查看其他可用的命令。

按下 `enter` 键且不输入命令，则可重复上一个调试命令。

