<!-- YAML
added: v10.0.0
-->

* `...streams` {Stream} 两个或多个要用管道连接的流
* `callback` {Function} 一个回调函数，可以带有一个错误信息参数

该模块方法用于在多个流之间架设管道，可以自动传递错误和完成扫尾工作，并且可在管道架设完成时提供一个回调函数：

```js
const { pipeline } = require('stream');
const fs = require('fs');
const zlib = require('zlib');

// 使用 pipeline API 轻松连接多个流
// 并在管道完成时获得通知

// 使用pipeline高效压缩一个可能很大的tar文件：

pipeline(
  fs.createReadStream('archive.tar'),
  zlib.createGzip(),
  fs.createWriteStream('archive.tar.gz'),
  (err) => {
    if (err) {
      console.error('管道架设失败', err);
    } else {
      console.log('管道架设成功');
    }
  }
);
```

`pipeline` API 也可做成承诺：

```js
const pipeline = util.promisify(stream.pipeline);

async function run() {
  await pipeline(
    fs.createReadStream('archive.tar'),
    zlib.createGzip(),
    fs.createWriteStream('archive.tar.gz')
  );
  console.log('管道架设成功');
}

run().catch(console.error);
```

