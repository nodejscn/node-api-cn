<!-- YAML
added: v0.4.0
-->

* {number}

当使用隐式的响应头时（没有显式地调用 [`response.writeHead()`]），该属性控制响应头刷新时将被发送到客户端的状态码。

例子：

```js
response.statusCode = 404;
```

响应头被发送到客户端后，该属性表示被发出的状态码。

