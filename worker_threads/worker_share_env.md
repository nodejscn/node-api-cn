<!-- YAML
added: v11.14.0
-->

* {symbol}

传递给构造函数[`Worker`][]选项对象`env`属性的值，用以指定主线程与工作线程将可共享环境变量的读写。

```js
const { Worker, SHARE_ENV } = require('worker_threads');
new Worker('process.env.SET_IN_WORKER = "foo"', { eval: true, env: SHARE_ENV })
  .on('exit', () => {
    console.log(process.env.SET_IN_WORKER);  // Prints 'foo'.
  });
```

