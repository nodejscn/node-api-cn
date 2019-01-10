<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {Buffer|Uint8Array|string|null|any} 要推入读取队列的数据块。
  对于非对象模式的流，`chunk` 必须是字符串、`Buffer` 或 `Uint8Array`。
  对于对象模式的流，`chunk` 可以是任何 JavaScript 值。
* `encoding` {string} 字符串数据块的字符编码。
  必须是有效的 `Buffer` 字符编码，例如 `'utf8'` 或 `'ascii'`。
* 返回: {boolean} 如果还有数据块可以继续推入，则返回 `true`，否则返回 `false`。

当 `chunk` 是 `Buffer`、`Uint8Array` 或字符串时，`chunk` 的数据会被添加到内部队列中供流消费。
在没有数据可写入后，给 `chunk` 传入 `null` 表示流的结束（EOF）。

当可读流处在暂停模式时，使用 `readable.push()` 添加的数据可以在触发 [`'readable'`] 事件时通过调用 [`readable.read()`][stream-read] 读取。

当可读流处于流动模式时，使用 `readable.push()` 添加的数据可以通过触发 `'data'` 事件读取。

`readable.push()` 方法被设计得尽可能的灵活。
例如，当需要封装一个带有'暂停/继续'机制与数据回调的底层数据源时，该底层数据源可以使用自定义的可读流实例封装：

```js
// `source` 是一个有 `readStop()` 和 `readStart()` 方法的对象，
// 当有数据时会调用 `ondata` 方法，
// 当数据结束时会调用 `onend` 方法。

class SourceWrapper extends Readable {
  constructor(options) {
    super(options);

    this._source = getLowlevelSourceObject();

    // 每当有数据时，将其推入内部缓冲。
    this._source.ondata = (chunk) => {
      // 如果 push() 返回 `false`，则停止读取。
      if (!this.push(chunk))
        this._source.readStop();
    };

    // 当读取到尽头时，推入 `null` 表示流的结束。
    this._source.onend = () => {
      this.push(null);
    };
  }
  // 当流想推送更多数据时，`_read` 会被调用。
  _read(size) {
    this._source.readStart();
  }
}
```

`readable.push()` 只能被可读流的实现调用，且只能在 `readable._read()` 方法中调用。

对于非对象模式的流，如果 `readable.push()` 的 `chunk` 参数为 `undefined`，则它会被当成空字符串或 buffer。
详见 [`readable.push('')`]。


