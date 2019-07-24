<!-- YAML
added: v10.12.0
-->

* `filename` {string} 用于构造通过相对路径加载模块的函数的文件名。
* 返回: {[`require`][]} 加载模块的函数。

```js
const { createRequireFromPath } = require('module');
const requireUtil = createRequireFromPath('../src/utils');

// require `../src/utils/some-tool`
requireUtil('./some-tool');
```












