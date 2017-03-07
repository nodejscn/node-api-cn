<!-- YAML
added: v0.11.0
-->

The `'reset'` event is emitted when the REPL's context is reset. This occurs
whenever the `.clear` command is received as input *unless* the REPL is using
the default evaluator and the `repl.REPLServer` instance was created with the
`useGlobal` option set to `true`. The listener callback will be called with a
reference to the `context` object as the only argument.
REPL的上下文环境复位时，触发`‘reset'`事件。当输入收到`.clear`命令后触发，*除非*REPL正式用默认的解释器并且`repl.REPLServer`实例创建时设置`useGlobal`选项为`true`
监听的回调函数被调用，`context`对象的引用是惟一的参数。

This can be used primarily to re-initialize REPL context to some pre-defined
state as illustrated in the following simple example:
这可被主要用于重新初始化REPL上下文，使之达到某些预定义的状态，如下面的例子：

```js
const repl = require('repl');

function initializeContext(context) {
  context.m = 'test';
}

var r = repl.start({prompt: '>'});
initializeContext(r.context);

r.on('reset', initializeContext);
```

When this code is executed, the global `'m'` variable can be modified but then
reset to its initial value using the `.clear` command:
当这个代码被执行后，全局的`'m'`变量会被修改，但随后的`.clear`命令会把它复位到初始化值

```js
$ ./node example.js
>m
'test'
>m = 1
1
>m
1
>.clear
Clearing context...
>m
'test'
>
```

