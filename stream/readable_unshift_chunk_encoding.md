<!-- YAML
added: v0.9.11
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {Buffer|Uint8Array|string|null|any} 要推回可读队列的数据块。
	对于非对象模式的流，`chunk` 必须是字符串、`Buffer`、`Uint8Array` 或 `null`。
	对于对象模式的流，`chunk` 可以是任何 JavaScript 值。
* `encoding` {string} 字符串块的编码。 必须是有效的 `Buffer` 编码，例如 `'utf8'` 或 `'ascii'`。

将 `chunk` 作为 `null` 传递信号表示流的末尾（EOF），之后不能再写入数据。

`readable.unshift()` 方法将数据块推回内部缓冲。
可用于以下情景：正被消费中的流需要将一些已经被拉出的数据重置为未消费状态，以便这些数据可以传给其他方。

触发 [`'end'`] 事件或抛出运行时错误之后，不能再调用 `stream.unshift()` 方法。

使用 `stream.unshift()` 的开发者可以考虑切换到 [`Transform`] 流。
详见[用于实现流的API][API for Stream Implementers]。

```js
// 拉出由 \n\n 分隔的标题。
// 如果获取太多，则使用 unshift()。
// 使用 (error, header, stream) 调用回调。
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

与 [`stream.push(chunk)`][stream-push] 不同，`stream.unshift(chunk)` 不会通过重置流的内部读取状态来结束读取过程。 
如果在读取期间调用 `readable.unshift()`（即从自定义的流上的 [`stream._read()`][stream-_read] 实现中调用），则会导致意外结果。 
在使用立即的 [`stream.push('')`][stream-push] 调用 `readable.unshift()` 之后，将适当地重置读取状态，但最好在执行读取的过程中避免调用 `readable.unshift()`。

