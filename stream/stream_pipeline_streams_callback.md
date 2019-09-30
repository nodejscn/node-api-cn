<!-- YAML
added: v10.0.0
-->

* `...streams` {Stream} 要使用管道传送的两个或多个流。
* `callback` {Function} 当管道完全地完成时调用。
  * `err` {Error}

一个模块方法，使用管道传送多个流，并转发错误和正确地清理，当管道完成时提供回调。

```js
const { pipeline } = require('stream');
const fs = require('fs');
const zlib = require('zlib');

// 使用 pipeline API 轻松地将一系列的流通过管道一起传送，并在管道完全地完成时获得通知。

// 使用 pipeline 可以有效地压缩一个可能很大的 tar 文件：

pipeline(
  fs.createReadStream('archive.tar'),
  zlib.createGzip(),
  fs.createWriteStream('archive.tar.gz'),
  (err) => {
    if (err) {
      console.error('管道传送失败', err);
    } else {
      console.log('管道传送成功');
    }
  }
);
```

`pipeline` API 也可以 promise 化：

```js
const pipeline = util.promisify(stream.pipeline);

async function run() {
  await pipeline(
    fs.createReadStream('archive.tar'),
    zlib.createGzip(),
    fs.createWriteStream('archive.tar.gz')
  );
  console.log('管道传送成功');
}

run().catch(console.error);
```

在调用 `callback` 之后，`stream.pipeline()` 会将悬挂的事件监听器留在流上。
在失败后重新使用流的情况下，这可能导致事件监听器泄漏和误吞的错误。

