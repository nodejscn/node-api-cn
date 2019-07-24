<!-- YAML
added: v10.0.0
-->

* `stream` {Stream} 可读流或可写流。
* `callback` {Function} 通知回调函数。

当流不再可读、可写、发生错误、或提前关闭时，通过该函数获得通知。

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

