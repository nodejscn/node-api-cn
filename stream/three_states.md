
可读流的“两种操作模式”是一种简单抽象。它抽象了在可读流实现（Readable stream implementation）内部发生的复杂的状态管理过程。

在任意时刻，任意可读流应确切处于下面三种状态之一：

* `readable._readableState.flowing = null`
* `readable._readableState.flowing = false`
* `readable._readableState.flowing = true`

若 `readable._readableState.flowing` 为 `null`，由于不存在数据消费者，可读流将不会产生数据。
在这个状态下，监听 `'data'` 事件，调用 `readable.pipe()`
方法，或者调用 `readable.resume()` 方法，
`readable._readableState.flowing` 的值将会变为 `true` 。这时，随着数据生成，可读流开始频繁触发事件。

调用 `readable.pause()` 方法， `readable.unpipe()` 方法， 或者接收 “背压”（back pressure），
将导致 `readable._readableState.flowing` 值变为 `false`。
这将暂停事件流，但 *不会* 暂停数据生成。
在这种情况下，为 `'data'` 事件设置监听函数不会导致
 `readable._readableState.flowing` 变为 `true`。

```js
const { PassThrough, Writable } = require('stream');
const pass = new PassThrough();
const writable = new Writable();

pass.pipe(writable);
pass.unpipe(writable);
// flowing 现在为 false

pass.on('data', (chunk) => { console.log(chunk.toString()); });
pass.write('ok'); // 不会触发 'data' 事件
pass.resume(); // 只有被调用了才会触发 'data' 事件
```

当 `readable._readableState.flowing` 值为 `false` 时， 数据可能堆积到流的内部缓存中。

