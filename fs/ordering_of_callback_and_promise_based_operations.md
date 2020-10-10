
当使用异步的方法时，无法保证顺序。
因此，以下的操作容易出错，因为 `fs.stat()` 操作可能在 `fs.rename()` 操作之前完成：


```js
fs.rename('旧文件', '新文件', (err) => {
  if (err) throw err;
  console.log('重命名完成');
});
fs.stat('新文件', (err, stats) => {
  if (err) throw err;
  console.log(`文件属性: ${JSON.stringify(stats)}`);
});
```

若要正确地排序这些操作，则移动 `fs.stat()` 调用到 `fs.rename()` 操作的回调中：

```js
fs.rename('旧文件', '新文件', (err) => {
  if (err) throw err;
  fs.stat('新文件', (err, stats) => {
    if (err) throw err;
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  });
});
```

或者，使用基于 promise 的 API：

```js
const fs = require('fs/promises');

(async function(from, to) {
  try {
    await fs.rename(from, to);
    const stats = await fs.stat(to);
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  } catch (error) {
    console.error('出错：', error.message);
  }
})('旧文件', '新文件');
```

