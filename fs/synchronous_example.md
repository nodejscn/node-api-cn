
同步的形式会阻塞 Node.js 事件循环和进一步的 JavaScript 执行，直到操作完成。 
异常会被立即地抛出，可以使用 `try…catch` 处理，也可以冒泡。

```js
const fs = require('fs');

try {
  fs.unlinkSync('文件');
  console.log('已成功删除文件');
} catch (err) {
  // 处理错误
}
```
