<!-- YAML
added: v10.0.0
-->

* `stream` {Stream} 可读和/或可写流。
* `options` {Object}
  * `error` {boolean} 如果设置为 `false`，则对 `emit('error', err)` 的调用不会被视为已完成。 **默认值**: `true`。
  * `readable` {boolean} 当设置为 `false` 时，即使流可能仍然可读，当流结束时也将会调用回调。**默认值**: `true`。
  * `writable` {boolean} 当设置为 `false` 时，即使流可能仍然可写，当流结束时也将会调用回调。**默认值**: `true`。
* `callback` {Function} 带有可选错误参数的回调函数。
* 返回: {Function} 清理函数，它会移除所有已注册的监听器。

当流不再可读、可写、或遇到错误、或过早关闭事件时，则该函数会获得通知。

```js
const { finished } = require('stream');

const rs = fs.createReadStream('archive.tar');

finished(rs, (err) => {
  if (err) {
    console.error('流读取失败', err);
  } else {
    console.log('流已完成读取');
  }
});

rs.resume(); // 排空流。
```

在错误处理场景中特别有用，该场景中的流会被过早地销毁（例如被终止的 HTTP 请求），并且不会触发 `'end'` 或 `'finish'` 事件。

`finished` API 也可以 promise 化：

```js
const finished = util.promisify(stream.finished);

const rs = fs.createReadStream('archive.tar');

async function run() {
  await finished(rs);
  console.log('流已完成读取');
}

run().catch(console.error);
rs.resume(); // 排空流。
```

在调用 `callback` 之后，`stream.finished()` 会留下悬挂的事件监听器（特别是 `'error'`、`'end'`、`'finish'` 和 `'close'`）。
这样做的原因是，意外的 `'error'` 事件（由于错误的流实现）不会导致意外的崩溃。
如果这是不想要的行为，则需要在回调中调用返回的清理函数：

```js
const cleanup = finished(rs, (err) => {
  cleanup();
  // ...
});
```

