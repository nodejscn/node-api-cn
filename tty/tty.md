
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!-- source_link=lib/tty.js -->

`tty` 模块提供了 `tty.ReadStream` 和 `tty.WriteStream` 类。 
在大多数情况中，不需要也不可能直接地使用此模块。 
当然，它可以被使用以下方式访问：

```js
const tty = require('tty');
```

当 Node.js 检测到它被运行时附加了一个文本终端（TTY），则默认情况下，[`process.stdin`] 会被初始化为 `tty.ReadStream` 的实例，[`process.stdout`] 和 [`process.stderr`] 会被初始化为 `tty.WriteStream` 的实例。 
判断 Node.js 是否被运行在一个 TTY 上下文中的首选方法是检查 `process.stdout.isTTY` 属性的值是否为 `true`：

```console
$ node -p -e "Boolean(process.stdout.isTTY)"
true
$ node -p -e "Boolean(process.stdout.isTTY)" | cat
false
```

在大多数情况下，应用程序几乎没有理由手动地创建 `tty.ReadStream` 和 `tty.WriteStream` 类的实例。

