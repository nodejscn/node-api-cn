
基于 promise 的操作会返回 `Promise`（当异步操作完成时被解决）。

```js
const fs = require('fs/promises');

(async function(path) {
  try {
    await fs.unlink(path);
    console.log(`已成功地删除文件 ${path}`);
  } catch (error) {
    console.error('出错：', error.message);
  }
})('文件');
```

