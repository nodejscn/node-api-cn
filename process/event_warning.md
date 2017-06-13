<!-- YAML
added: v6.0.0
-->

任何时候Node.js发出进程告警，都会触发`'warning'`事件。

进程告警与进程错误的相似之处，在于两者都描述了需要引起用户注意的异常条件。
区别在于，告警不是Node.js和Javascript错误处理流程的正式组成部分。
一旦探测到可能导致应用性能问题，缺陷或安全隐患相关的代码实践，Node.js就可发出告警。

`'warning'`事件监听器的回调函数，参数只有一个，其值为`Error` 对象。此对象有三个重要的属性用来描述告警：
* `name` {string} 告警的名称(目前默认值是 `Warning`)。
* `message` {string} 系统提供的对此告警的描述。
* `stack` {string} 当告警触发时，包含代码位置的堆栈信息。

```js
process.on('warning', (warning) => {
  console.warn(warning.name);    // Print the warning name
  console.warn(warning.message); // Print the warning message
  console.warn(warning.stack);   // Print the stack trace
});
```

默认Node.js会打印进程告警到`stderr`。使用`--no-warnings`的命令行选项可以阻止默认从console输出信息，
但是`'warning'`事件仍然会被`process`对象发出。

下面的例子展示了当一个事件绑定了太多的监听器时，输出到`stderr`的告警。

```txt
$ node
> events.defaultMaxListeners = 1;
> process.on('foo', () => {});
> process.on('foo', () => {});
> (node:38638) MaxListenersExceededWarning: Possible EventEmitter memory leak
detected. 2 foo listeners added. Use emitter.setMaxListeners() to increase limit
```

与上述相反，如下例子关闭了默认的告警输出，并且给`'warning'`事件添加了一个定制的处理器。

```txt
$ node --no-warnings
> const p = process.on('warning', (warning) => console.warn('Do not do that!'));
> events.defaultMaxListeners = 1;
> process.on('foo', () => {});
> process.on('foo', () => {});
> Do not do that!
```

`--trace-warnings`命令行选项可以让默认的console输出告警信息时，包含告警的全部堆栈信息。

使用`--throw-deprecation`命令行选项标志启动Node.js，会使得custom deprecation warning作为异常信息抛出来。

使用`--trace-deprecation`命令行选项标志，会使得custom deprecation warning打印到`stderr`，包括其堆栈信息。

使用`--trace-deprecation`命令行选项标志，会阻止报告所有的custom deprecation warning。

`*-deprecation` 命令行选项标志，只会影响使用名字为`DeprecationWarning`的告警。
