<!-- YAML
added: v0.9.4
-->

* `encoding` {string} 要使用的编码
* Returns: `this`

`readble.setEncoding()` 方法会为从可读流读入的数据设置字符编码

By default, no encoding is assigned and stream data will be returned as
`Buffer` objects.
设置编码会使得该流数据返回指定编码的字符串而不是`Buffer`对象。例如，调用`readable.setEncoding('utf-8')`会使得输出数据作为UTF-8数据解析，并作为字符串返回。调用`readable.setEncoding('hex')`使得数据被编码成16进制字符串格式。

可读流会妥善处理多字节字符，如果仅仅直接从流中取出`Buffer`对象，很可能会导致错误解码。

```js
const readable = getReadableStreamSomehow();
readable.setEncoding('utf8');
readable.on('data', (chunk) => {
  assert.equal(typeof chunk, 'string');
  console.log('got %d characters of string data', chunk.length);
});
```

