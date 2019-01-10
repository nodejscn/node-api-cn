<!-- YAML
added: v0.11.0
-->

当 REPL 的上下文被重置时，触发 `'reset'` 事件。
每当接收到 `.clear` 命令时会触发该事件，除非 REPL 正在使用默认的解释器并且 `repl.REPLServer` 实例被创建时 `useGlobal` 选项被设为 `true`。
监听器的回调函数被调用时会带上 `context` 对象作为惟一的参数。

这主要被用于重新初始化 REPL 上下文，使之达到某些预定义的状态，如下面的例子：

```js
const repl = require('repl');

function initializeContext(context) {
  context.m = 'test';
}

const r = repl.start({ prompt: '> ' });
initializeContext(r.context);

r.on('reset', initializeContext);
```

当代码被执行时，全局的 `'m'` 变量可以被修改，但随后的 `.clear` 命令会把它重置回初始值：

<!-- eslint-skip -->
```js
$ ./node example.js
> m
'test'
> m = 1
1
> m
1
> .clear
Clearing context...
> m
'test'
>
```

