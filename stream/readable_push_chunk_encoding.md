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

When `chunk` is a `Buffer`, `Uint8Array` or `string`, the `chunk` of data will
be added to the internal queue for users of the stream to consume.
Passing `chunk` as `null` signals the end of the stream (EOF), after which no
more data can be written.

When the Readable is operating in paused mode, the data added with
`readable.push()` can be read out by calling the
[`readable.read()`][stream-read] method when the [`'readable'`][] event is
emitted.

When the Readable is operating in flowing mode, the data added with
`readable.push()` will be delivered by emitting a `'data'` event.

The `readable.push()` method is designed to be as flexible as possible. For
example, when wrapping a lower-level source that provides some form of
pause/resume mechanism, and a data callback, the low-level source can be wrapped
by the custom Readable instance as illustrated in the following example:

```js
// source is an object with readStop() and readStart() methods,
// and an `ondata` member that gets called when it has data, and
// an `onend` member that gets called when the data is over.

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
*Note*: The `readable.push()` method is intended be called only by Readable
Implementers, and only from within the `readable._read()` method.

