<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {Buffer|Uint8Array|string|null|any} 压入读队列的数据块。
  对于没有处在object mode的流来说，`chunk`必须是一个字符串，`Buffer` 或`Uint8Array`；
  对object mode 的流来说，`chunk`可以使任何JavaScript值。
* `encoding` {string} 字符串数据块的编码方式.  必须是可用的Buffer编码方式，例如`'utf8'` 或 `'ascii'`。
* 返回 {boolean} 如果多余的数据块可能会继续压入，那么返回`true`; 否则返回 `false`.

当`chunk`是一个`Buffer`, `Uint8Array`或者`string`时，
这个数据块(`chunk`)会被添加到内部队列供使用者消费。
在没有数据可写入后，给`chunk`传了`null`发出流结束(EOF)的信号。

当可读流处在传输模式下，`'data'`事件触发时，可以通过
调用[`readable.read()`][stream-read] 方法读出来数据，这数据是用`readable.push()`添加的。

`readable.push()`方法被设计得尽可能的灵活。
比如，当封装一个有'暂停/恢复'机制和带数据回调的底层source的时候，
那么这个底层的source可以被常规的可读流实例封装。就像下面的例子一样。


```js
// source 是一个有readStop()和 readStart()方法的对象。
// 有数据就调`ondata`成员函数；
// 数据结束就调`onend`成员函数。

class SourceWrapper extends Readable {
  constructor(options) {
    super(options);

    this._source = getLowlevelSourceObject();

    // Every time there's data, push it into the internal buffer.
    this._source.ondata = (chunk) => {
      // if push() returns false, then stop reading from source
      if (!this.push(chunk))
        this._source.readStop();
    };

    // When the source ends, push the EOF-signaling `null` chunk
    this._source.onend = () => {
      this.push(null);
    };
  }
  // _read will be called when the stream wants to pull more data in
  // the advisory size argument is ignored in this case.
  _read(size) {
    this._source.readStart();
  }
}
```
*注意*: `readable.push()`方法是为了让可读流实现者调用的，
而且只来自`readable._read()`方法内部。

