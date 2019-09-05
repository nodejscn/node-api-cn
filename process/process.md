
<!-- introduced_in=v0.10.0 -->
<!-- type=global -->

`process` 对象是一个全局变量，它提供有关当前 Node.js 进程的信息并对其进行控制。 
作为一个全局变量，它始终可供 Node.js 应用程序使用，无需使用 `require()`。
它也可以使用 `require()` 显式地访问：

```js
const process = require('process');
```

