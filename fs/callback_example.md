
异步的形式总是把完成回调作为其最后一个参数。
传给完成回调的参数取决于具体方法，但第一个参数总是预留给异常。
如果操作被成功地完成，则第一个参数会为 `null` 或 `undefined`。

```js
const fs = require('fs');

fs.unlink('文件', (err) => {
  if (err) throw err;
  console.log('已成功地删除文件');
});
```

