<!-- YAML
added: v0.4.0
-->

* {Number}

当使用隐式的消息头时（没有显式地调用 [`response.writeHead()`]），在消息头被刷新时该属性会控制将被发送到客户端的状态码。

例子：

```js
response.statusCode = 404;
```

响应头被发送到客户端后，该属性表明被发出的状态码。

