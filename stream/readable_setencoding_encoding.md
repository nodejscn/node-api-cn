<!-- YAML
added: v0.9.4
-->

* `encoding` {string} 字符编码。
* 返回: {this}

为从可读流读取的数据设置字符编码。

默认情况下没有设置字符编码，流数据返回的是 `Buffer` 对象。
如果设置了字符编码，则流数据返回指定编码的字符串。
例如，调用 `readable.setEncoding('utf-8')` 会将数据解析为 UTF-8 数据，并返回字符串，调用 `readable.setEncoding('hex')` 则会将数据编码成十六进制字符串。

```js
const readable = getReadableStreamSomehow();
readable.setEncoding('utf8');
readable.on('data', (chunk) => {
  assert.equal(typeof chunk, 'string');
  console.log('读取到 %d 个字符的字符串数据', chunk.length);
});
```

