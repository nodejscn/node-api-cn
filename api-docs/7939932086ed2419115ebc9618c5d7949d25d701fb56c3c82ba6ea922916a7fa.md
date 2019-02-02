
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`tty` 模块提供 `tty.ReadStream` 和 `tty.WriteStream` 类。 
在大多数情况下，没有必要或可能直接使用此模块。 
可以使用以下方法访问它：

```js
const tty = require('tty');
```

当 Node.js 检测到它附加了文本终端（TTY）时，默认情况下，[`process.stdin`] 将被初始化为 `tty.ReadStream` 的一个实例，[`process.stdout`] 和 [`process.stderr`] 将被初始化为 `tty.WriteStream` 的实例。 
判断 Node.js 是否在 TTY 上下文中运行的首选方法是检查 `process.stdout.isTTY` 属性的值是否为 `true`：

```sh
$ node -p -e "Boolean(process.stdout.isTTY)"
true
$ node -p -e "Boolean(process.stdout.isTTY)" | cat
false
```

在大多数情况下，应用程序应该几乎没有理由手动创建 `tty.ReadStream` 和 `tty.WriteStream` 类的实例。

