
默认的解释器会自动加载被调用的 Node.js 核心模块到 REPL 环境中。
例如，除非被声明为一个全局变量或一个有限范围的变量，否则输入 `fs` 会被解释为 `global.fs = require('fs')`。

<!-- eslint-skip -->
```js
> fs.createReadStream('./some/file');
```

