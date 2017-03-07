
The default evaluator will automatically load Node.js core modules into the
REPL environment when used. For instance, unless otherwise declared as a
global or scoped variable, the input `fs` will be evaluated on-demand as
`global.fs = require('fs')`.

默认的解释器会自动装载被调用的Node.js核心模块到REPL环境中。举个例子，除了声明为
全局或有限范围的变量的情况，输入`fs`会被解释为
`global.fs = require('fs')`.


```js
> fs.createReadStream('./some/file');
```

