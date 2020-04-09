

除显式同步的 API 之外，所有 `zlib` API 均使用 Node.js 内部的线程池。 
这可能会在某些应用程序中产生意外的效果或性能限制。

同时创建和使用大量的 zlib 对象可能会导致明显的内存碎片。


```js
const zlib = require('zlib');

const payload = Buffer.from('这是一些数据');

// 警告：请勿这样做！
for (let i = 0; i < 30000; ++i) {
  zlib.deflate(payload, (err, buffer) => {});
}
```

在前面的示例中，同时创建了 30,000 个 deflate 实例。 
由于某些操作系统处理内存分配和释放的方式，因此可能会导致内存碎片严重。

强烈建议对压缩操作的结果进行缓存，以避免重复工作。

