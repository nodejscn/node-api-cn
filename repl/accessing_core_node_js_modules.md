
默认的解释器会自动装载被调用的 Node.js 核心模块到 REPL 环境中。
举个例子，除了声明为全局或有限范围的变量的情况，输入`fs`会被解释为 `global.fs = require('fs')`。

```js
> fs.createReadStream('./some/file');
```

