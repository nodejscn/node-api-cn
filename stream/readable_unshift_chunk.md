<!-- YAML
added: v0.9.11
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {Buffer|Uint8Array|string|any} 数据块移动到可读队列底部。对于不以对象模式运行的流，`chunk` 必须是字符串， `Buffer` 或者 `Uint8Array`。对于对象流， `chunk` 任何非`null`的值。

`readable.unshift()` 方法会提交一个数据块到`Buffer`内部。 This is useful in certain situations where a stream is being consumed by
code that needs to "un-consume" some amount of data that it has optimistically
pulled out of the source, so that the data can be passed on to some other party.

*Note*: The `stream.unshift(chunk)` method cannot be called after the
[`'end'`][] event has been emitted or a runtime error will be thrown.

Developers using `stream.unshift()` often should consider switching to
use of a [Transform][] stream instead. See the [API for Stream Implementers][]
section for more information.

```js
// Pull off a header delimited by \n\n
// use unshift() if we get too much
// Call the callback with (error, header, stream)
const { StringDecoder } = require('string_decoder');
function parseHeader(stream, callback) {
  stream.on('error', callback);
  stream.on('readable', onReadable);
  const decoder = new StringDecoder('utf8');
  let header = '';
  function onReadable() {
    let chunk;
    while (null !== (chunk = stream.read())) {
      const str = decoder.write(chunk);
      if (str.match(/\n\n/)) {
        // found the header boundary
        const split = str.split(/\n\n/);
        header += split.shift();
        const remaining = split.join('\n\n');
        const buf = Buffer.from(remaining, 'utf8');
        stream.removeListener('error', callback);
        // remove the readable listener before unshifting
        stream.removeListener('readable', onReadable);
        if (buf.length)
          stream.unshift(buf);
        // now the body of the message can be read from the stream.
        callback(null, header, stream);
      } else {
        // still reading the header.
        header += str;
      }
    }
  }
}
```

*Note*: Unlike [`stream.push(chunk)`][stream-push], `stream.unshift(chunk)`
will not end the reading process by resetting the internal reading state of the
stream. This can cause unexpected results if `readable.unshift()` is called
during a read (i.e. from within a [`stream._read()`][stream-_read]
implementation on a custom stream). Following the call to `readable.unshift()`
with an immediate [`stream.push('')`][stream-push] will reset the reading state
appropriately, however it is best to simply avoid calling `readable.unshift()`
while in the process of performing a read.

