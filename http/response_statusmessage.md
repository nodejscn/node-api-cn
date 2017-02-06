<!-- YAML
added: v0.11.8
-->

* {String}

当使用隐式的消息头时（没有显式地调用 [`response.writeHead()`]），在消息头被刷新时该属性会控制将被发送到客户端的状态信息。
如果该值为 `undefined`，则使用状态码的标准信息。

例子：

```js
response.statusMessage = 'Not found';
```

响应头被发送到客户端后，该属性表明被发出的状态信息。

