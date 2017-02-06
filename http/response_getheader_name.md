<!-- YAML
added: v0.4.0
-->

* `name` {String}
* 返回: {String}

读出已经排队但尚未发送到客户端的消息头。
注意，名称不区分大小写。
只能在消息头被隐式地刷新前调用。

例子：

```js
var contentType = response.getHeader('content-type');
```

