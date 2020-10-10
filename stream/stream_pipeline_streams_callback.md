<!-- YAML
added: v10.0.0
changes:
  - version: v13.10.0
    pr-url: https://github.com/nodejs/node/pull/31223
    description: Add support for async generators.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/32158
    description: The `pipeline(..., cb)` will wait for the `'close'` event
                 before invoking the callback. The implementation tries to
                 detect legacy streams and only apply this behavior to streams
                 which are expected to emit `'close'`.
-->

* `streams` {Stream[]|Iterable[]|AsyncIterable[]|Function[]}
* `source` {Stream|Iterable|AsyncIterable|Function}
  * Returns: {Iterable|AsyncIterable}
* `...transforms` {Stream|Function}
  * `source` {AsyncIterable}
  * Returns: {AsyncIterable}
* `destination` {Stream|Function}
  * `source` {AsyncIterable}
  * Returns: {AsyncIterable|Promise}
* `callback` {Function} 当管道完全地完成时调用。
  * `err` {Error}
  * `val` `destination` 返回的 `Promise` 的 resolve 的值。 
* 返回: {Stream}

一个模块方法，使用管道传送多个流和生成器，并转发错误和正确地清理，当管道完成时提供回调。

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

`pipeline` API 还支持异步的生成器：

```js
const pipeline = util.promisify(stream.pipeline);
const fs = require('fs');

async function run() {
  await pipeline(
    fs.createReadStream('lowercase.txt'),
    async function* (source) {
      source.setEncoding('utf8');  // Work with strings rather than `Buffer`s.
      for await (const chunk of source) {
        yield chunk.toUpperCase();
      }
    },
    fs.createWriteStream('uppercase.txt')
  );
  console.log('Pipeline 成功');
}

run().catch(console.error);
```

`stream.pipeline()` 将会在所有的流上调用 `stream.destroy(err)`，除了：
* 已触发 `'end'` 或 `'close'` 的 `Readable` 流。
* 已触发 `'finish'` 或 `'close'` 的 `Writable` 流。

在调用 `callback` 之后，`stream.pipeline()` 会将悬挂的事件监听器留在流上。
在失败后重新使用流的情况下，这可能导致事件监听器泄漏和误吞的错误。

