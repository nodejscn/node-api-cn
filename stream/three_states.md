
可读流的两种模式是对发生在可读流中更加复杂的内部状态管理的一种简化的抽象。

在任意时刻，可读流会处于以下三种状态之一：

* `readable.readableFlowing === null`
* `readable.readableFlowing === false`
* `readable.readableFlowing === true`

当 `readable.readableFlowing` 为 `null` 时，没有提供消费流数据的机制，所以流不会产生数据。
在这个状态下，监听 `'data'` 事件、调用 `readable.pipe()`、或调用 `readable.resume()` 都会使 `readable.readableFlowing` 切换到 `true`，可读流开始主动地产生数据并触发事件。

调用 `readable.pause()`、`readable.unpipe()`、或接收到背压，则 `readable.readableFlowing` 会被设为 `false`，暂时停止事件流动但不会停止数据的生成。
在这个状态下，为 `'data'` 事件绑定监听器不会使 `readable.readableFlowing` 切换到 `true`。

```js
const { PassThrough, Writable } = require('stream');
const pass = new PassThrough();
const writable = new Writable();

pass.pipe(writable);
pass.unpipe(writable);
// readableFlowing 现在为 false。

pass.on('data', (chunk) => { console.log(chunk.toString()); });
pass.write('ok'); // 不会触发 'data' 事件。
pass.resume(); // 必须调用它才会触发 'data' 事件。
```

当 `readable.readableFlowing` 为 `false` 时，数据可能会堆积在流的内部缓冲中。

