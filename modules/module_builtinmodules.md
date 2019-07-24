<!-- YAML
added: v9.3.0
-->

* {string[]}

罗列 Node.js 提供的所有模块名称。可以用来判断模块是否为第三方所维护。

注意，`module` 在此处含义与[模块封装器][module wrapper]所提供的 `module` 是不同的。可以通过引入 `Module` 模块访问：

```js
const builtin = require('module').builtinModules;
```

