<!-- YAML
added: v0.11.8
-->

* {string}

当使用隐式的响应头时（没有显式地调用 [`response.writeHead()`]），此属性控制在刷新响应头时将发送到客户端的状态消息。 
如果保留为 `undefined`，则将使用状态码的标准消息。

```js
response.statusMessage = 'Not found';
```

响应头发送到客户端后，此属性表示已发送的状态消息。

