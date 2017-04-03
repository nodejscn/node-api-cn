<!-- YAML
added: v0.9.4
-->

* `encoding` {String} 要使用的编码
* Returns: `this`

`readble.setEncoding()` 方法会为从Readable stream 读入的数据设置默认字符编码

Setting an encoding causes the stream data
to be returned as string of the specified encoding rather than as `Buffer`
objects. For instance, calling `readable.setEncoding('utf8')` will cause the
output data will be interpreted as UTF-8 data, and passed as strings. Calling
`readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal
string format.

设置编码会使得该流数据返回指定编码的字符串而不是`Buffer`对象。例如，调用`readable.setEncoding('utf-8')`会使得输出数据作为UTF-8数据解析，并作为字符串返回

The Readable stream will properly handle multi-byte characters delivered through
the stream that would otherwise become improperly decoded if simply pulled from
the stream as `Buffer` objects.

Encoding can be disabled by calling `readable.setEncoding(null)`. This approach
is useful when working with binary data or with large multi-byte strings spread
out over multiple chunks.

```js
const readable = getReadableStreamSomehow();
readable.setEncoding('utf8');
readable.on('data', (chunk) => {
  assert.equal(typeof chunk, 'string');
  console.log('got %d characters of string data', chunk.length);
});
```

