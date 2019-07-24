<!-- YAML
added: v0.3.0
-->

* `headers` {Object}

此方法将 HTTP 尾部响应头（一种在消息末尾的响应头）添加到响应中。

只有在使用分块编码进行响应时才会发出尾部响应头; 如果不是（例如，如果请求是 HTTP/1.0），它们将被静默丢弃。

请注意，HTTP 需要发送 `Trailer` 响应头才能发出尾部响应头，并在其值中包含响应头字段列表。 
例如：

```js
response.writeHead(200, { 'Content-Type': 'text/plain',
                          'Trailer': 'Content-MD5' });
response.write(fileData);
response.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
response.end();
```

尝试设置包含无效字符的响应头字段名称或值将导致抛出 [`TypeError`]。

