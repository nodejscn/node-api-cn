<!-- YAML
added: v0.9.11
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {Buffer|Uint8Array|string|any} 要推回可读队列的数据块。
	对于非对象模式的流，`chunk` 必须是字符串、`Buffer` 或 `Uint8Array`。
	对于对象模式的流，`chunk` 可以是任何值，除了 `null`。

将数据块推回内部缓冲。
可用于以下情景：正被消费中的流需要将一些已经被拉出的数据重置为未消费状态，以便这些数据可以传给其他方。

触发 [`'end'`] 事件或抛出运行时错误之后，不能再调用 `stream.unshift()`。

使用 `stream.unshift()` 的开发者可以考虑切换到 [`Transform`] 流。
详见[用于实现流的API][API for Stream Implementers]。

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
        // 发现头部边界。
        const split = str.split(/\n\n/);
        header += split.shift();
        const remaining = split.join('\n\n');
        const buf = Buffer.from(remaining, 'utf8');
        stream.removeListener('error', callback);
        // 在调用 unshift() 前移除 'readable' 监听器。
        stream.removeListener('readable', onReadable);
        if (buf.length)
          stream.unshift(buf);
        // 现在可以从流中读取消息的主体。
        callback(null, header, stream);
      } else {
        // 继续读取头部。
        header += str;
      }
    }
  }
}
```

