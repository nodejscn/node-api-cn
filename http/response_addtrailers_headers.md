<!-- YAML
added: v0.3.0
-->

* `headers` {Object}

该方法会给响应添加 HTTP 追踪请求头（一个在消息尾部的请求头）。

追踪**仅**当响应使用分块编码时才会被发送；如果不是（比如请求是 HTTP/1.0），则它们将被丢弃。

注意，如果想要发送追踪，则 HTTP 要求发送 `Trailer` 请求头，且在值里带上请求头字段的列表。
例如：

```js
response.writeHead(200, { 'Content-Type': 'text/plain',
                          'Trailer': 'Content-MD5' });
response.write(fileData);
response.addTrailers({'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667'});
response.end();
```

试图设置一个包含无效字符的请求头字段名称或值会导致抛出一个 [`TypeError`]。

