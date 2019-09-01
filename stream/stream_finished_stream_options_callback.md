<!-- YAML
added: v10.0.0
-->

* `stream` {Stream} 可读流或可写流。
* `options` {Object}
  * `error` {boolean} 如果设置为 `false`，则对 `emit('error', err)` 的调用不会被视为已完成。 **默认值**: `true`。
  * `readable` {boolean} 当设置为 `false` 时，即使流可能仍然可读，当流结束时也将会调用回调。**默认值**: `true`。
  * `writable` {boolean} 当设置为 `false` 时，即使流可能仍然可写，当流结束时也将会调用回调。**默认值**: `true`。
* `callback` {Function} 带有可选错误参数的回调函数。

当流不再可读、可写、或遇到错误、或过早关闭事件时，该函数会获得通知。

```js
const { finished } = require('stream');

const rs = fs.createReadStream('archive.tar');

finished(rs, (err) => {
  if (err) {
    console.error('流发生错误', err);
  } else {
    console.log('流已读取完');
  }
});

rs.resume(); // 开始读取流。
```

主要用于处理流被提前销毁（如 HTTP 请求被中止）等异常情况，此时流不会触发 `'end'` 或 `'finish'` 事件。

`finished` 接口也可以 Promise 化：

```js
const finished = util.promisify(stream.finished);

const rs = fs.createReadStream('archive.tar');

async function run() {
  await finished(rs);
  console.log('流已读取完');
}

run().catch(console.error);
rs.resume(); // 开始读取流。
```

