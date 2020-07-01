
以下常量由 `fs.constants` 输出。

并非所有操作系统都可以使用每个常量。


To use more than one constant, use the bitwise OR `|` operator.

Example:

```js
const fs = require('fs');

const {
  O_RDWR,
  O_CREAT,
  O_EXCL
} = fs.constants;

fs.open('/path/to/my/file', O_RDWR | O_CREAT | O_EXCL, (err, fd) => {
  // ...
});
```


