<!-- YAML
added: v10.0.0
-->

* `stream` {Stream} 一个可读或可写的流
* `callback` {Function} 一个回调函数，可以带有一个错误信息参数，也可没有

使用此函数，以在一个流不再可读、可写或发生了错误、提前关闭等事件时获得通知。

```js
const { finished } = require('stream');

const rs = fs.createReadStream('archive.tar');

finished(rs, (err) => {
  if (err) {
    console.error('流发生错误', err);
  } else {
    console.log('流已读完');
  }
});

rs.resume(); // 将流读完
```

在处理流的提前销毁（如被抛弃的HTTP请求）等错误事件时特别有用，此时流不会触发 `'end'` 或 `'finish'` 事件。

`finished` API 也可做成承诺：

```js
const finished = util.promisify(stream.finished);

const rs = fs.createReadStream('archive.tar');

async function run() {
  await finished(rs);
  console.log('流已读完');
}

run().catch(console.error);
rs.resume(); // 将流读完
```

