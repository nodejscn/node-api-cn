<!-- YAML
added: v12.2.0
-->

* `filename` {string|URL} 用于构造 require 函数的文件名。必须是一个文件 URL 对象、文件 URL 字符串、或绝对路径字符串。
* 返回: {require} require 函数。

```js
import { createRequire } from 'module';
const require = createRequire(import.meta.url);

// sibling-module.js 是一个 CommonJS 模块。
const siblingModule = require('./sibling-module');
```

