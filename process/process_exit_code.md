<!-- YAML
added: v0.1.13
-->

* `code` {integer} 结束状态码。默认为`0`。

`process.exit()`方法以结束状态码`code`指令Node.js同步终止进程。
如果`code`未提供，此exit方法要么使用'success' 状态码 `0`，要么使用`process.exitCode`属性值，前提是此属性已被设置。
Node.js在所有[`'exit'`]事件监听器都被调用了以后，才会终止进程。

使用一个'failure'状态码结束的例子:

```js
process.exit(1);
```

执行Node.js的shell应该会得到结束状态码`1`。

需要特别注意的是，调用`process.exit()`会强制进程尽快结束，*即使仍然有很多处于等待中的异步操作*没有全部执行完成，
*包括*输出到`process.stdout`和`process.stderr`的I/O操作。

在大多数情况下，显式调用`process.exit()`是没有必要的。如果在事件轮询队列中没有处于等待中的工作，Node.js进程会自行结束。
当进程正常结束时，`process.exitCode`属性可以被设置，以便于告知进程使用哪个结束状态码。

如下例子说明了一个 *错误使用* `process.exit()`方法的场景，会导致输出到stdout的数据清空或丢失：

```js
// This is an example of what *not* to do:
if (someConditionNotMet()) {
  printUsageToStdout();
  process.exit(1);
}
```

这个例子中出现问题的原因在于，Node.js中写入到`process.stdout`的操作有时是异步的，并可能在Node.js事件轮询的多个ticks中出现。
调用`process.exit()`会使得在写入`stdout`的额外操作执行*之前*，进程就被强制结束了。

与直接调用`process.exit()`相比，代码*应该*设置`process.exitCode`并允许进程自然的结束，以免事件轮询队列中存在额外的工作：

```js
// How to properly set the exit code while letting
// the process exit gracefully.
if (someConditionNotMet()) {
  printUsageToStdout();
  process.exitCode = 1;
}
```

如果出现错误情况，而有必要结束Node.js进程，抛出一个*uncaught*错误并且允许进程正常结束的处理方式，要比调用`process.exit()`安全的多。

