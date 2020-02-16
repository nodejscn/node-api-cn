<!-- YAML
added: v0.1.91
-->

* `options` {Object|string} 参阅 [`repl.start()`]。
* 继承自: {readline.Interface}

`repl.REPLServer` 的实例是使用 [`repl.start()`] 方法或直接使用 JavaScript 的 `new` 关键字创建。

```js
const repl = require('repl');

const options = { useColors: true };

const firstInstance = repl.start(options);
const secondInstance = new repl.REPLServer(options);
```

