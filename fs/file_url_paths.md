<!-- YAML
added: v7.6.0
-->
对于大多数 `fs` 模块的函数，`path` 或 `filename` 参数可以传入 WHATWG [`URL`] 对象。
仅支持使用 `file:` 协议的 [`URL`] 对象。

```js
const fs = require('fs');
const fileUrl = new URL('file:///文件');

fs.readFileSync(fileUrl);
```

`file:` URL 始终是绝对路径。


