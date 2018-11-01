<!-- YAML
added: v10.0.0
-->

* `...streams` {Stream} 要用管道连接的两个或多个流。
* `callback` {Function} 通知回调函数。

使用管道连接多个流，并传递错误与完成清理工作，当管道连接完成时通知回调函数。

```js
const { pipeline } = require('stream');
const fs = require('fs');
const zlib = require('zlib');

// 使用 pipeline 接口连接多个流，并在管道连接完成时获得通知。
// 使用 pipeline 可以高效地压缩一个可能很大的 tar 文件：

pipeline(
  fs.createReadStream('archive.tar'),
  zlib.createGzip(),
  fs.createWriteStream('archive.tar.gz'),
  (err) => {
    if (err) {
      console.error('管道连接失败', err);
    } else {
      console.log('管道连接成功');
    }
  }
);
```

`pipeline` 接口也可以 Promise 化：

```js
const pipeline = util.promisify(stream.pipeline);

async function run() {
  await pipeline(
    fs.createReadStream('archive.tar'),
    zlib.createGzip(),
    fs.createWriteStream('archive.tar.gz')
  );
  console.log('管道连接成功');
}

run().catch(console.error);
```

