
> 稳定性: 2 - 稳定的

`tty` 模块提供了 `tty.ReadStream` 类和 `tty.WriteStream` 类。
大多数情况下无需直接使用此模块。
它可以通过以下方式使用：

```js
const tty = require('tty');
```

当 Node.js 检测到它正被运行在一个文本终端（TTY）的上下文中时，则 `process.stdin` 默认会被初始化为一个 `tty.ReadStream` 实例，`process.stdout` 和 `process.stderr` 默认会被初始化为一个 `tty.WriteStream` 实例。
判断 Node.js 是否正被运行在一个 TTY 上下文中的首选方法是去检查 `process.stdout.isTTY` 属性的值是否为 `true`：


```sh
$ node -p -e "Boolean(process.stdout.isTTY)"
true
$ node -p -e "Boolean(process.stdout.isTTY)" | cat
false
```

大多数情况下，应用程序几乎没有理由创建 `tty.ReadStream` 类和 `tty.WriteStream` 类的实例。

