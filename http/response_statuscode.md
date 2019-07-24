<!-- YAML
added: v0.4.0
-->

* {number}

当使用隐式的响应头时（没有显式地调用 [`response.writeHead()`]），此属性控制在刷新响应头时将发送到客户端的状态码。

```js
response.statusCode = 404;
```

响应头发送到客户端后，此属性表示已发送的状态码。

