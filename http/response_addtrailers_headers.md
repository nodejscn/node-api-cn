<!-- YAML
added: v0.3.0
-->

* `headers` {Object}

该方法会添加 HTTP 尾部响应头（一种在消息尾部的响应头）到响应。

仅当响应使用分块编码时，尾部响应头才会被发送；否则（比如请求为 HTTP/1.0），尾部响应头会被丢弃。

注意，发送尾部响应头之前，需先发送 `Trailer` 响应头，并在值里带上尾部响应头字段的列表。
例如：

```js
response.writeHead(200, { 'Content-Type': 'text/plain',
                          'Trailer': 'Content-MD5' });
response.write(fileData);
response.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
response.end();
```

如果尾部响应头字段的名称或值包含无效字符，则抛出 [`TypeError`] 错误。

