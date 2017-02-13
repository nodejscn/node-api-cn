
> 稳定性: 2 - 稳定的

<!-- type=misc -->

Node.js 包含一个进程外的调试工具，可以通过[基于 TCP 的协议]和内置调试客户端访问。
要使用它，可以带上 `debug` 参数启动 Node.js，并带上需要调试的脚本的路径；然后会显示一个提示，表明成功启动调试器：

```txt
$ node debug myscript.js
< debugger listening on port 5858
connecting... ok
break in /home/indutny/Code/git/indutny/myscript.js:1
  1 x = 5;
  2 setTimeout(() => {
  3   debugger;
debug>
```

Node.js 的调试器客户端还未支持全部特性，但可以做些简单的步骤和检测。

在脚本的源代码中插入 `debugger;` 语句，则会在代码的那个位置启用一个断点：

```js
// myscript.js
x = 5;
setTimeout(() => {
  debugger;
  console.log('world');
}, 1000);
console.log('hello');
```

一旦运行调试器，则会在第 4 行出现一个断点：

```txt
$ node debug myscript.js
< debugger listening on port 5858
connecting... ok
break in /home/indutny/Code/git/indutny/myscript.js:1
  1 x = 5;
  2 setTimeout(() => {
  3   debugger;
debug> cont
< hello
break in /home/indutny/Code/git/indutny/myscript.js:3
  1 x = 5;
  2 setTimeout(() => {
  3   debugger;
  4   console.log('world');
  5 }, 1000);
debug> next
break in /home/indutny/Code/git/indutny/myscript.js:4
  2 setTimeout(() => {
  3   debugger;
  4   console.log('world');
  5 }, 1000);
  6 console.log('hello');
debug> repl
Press Ctrl + C to leave debug repl
> x
5
> 2+2
4
debug> next
< world
break in /home/indutny/Code/git/indutny/myscript.js:5
  3   debugger;
  4   console.log('world');
  5 }, 1000);
  6 console.log('hello');
  7
debug> quit
```

`repl` 命令用于运行代码。
`next` 命令用于步入下一行。
输入 `help` 可查看其他可用的命令。

按下 `enter` 键且不输入命令，可重复上一个调试命令。

