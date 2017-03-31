<!-- YAML
added: v0.4.0
-->

* `name` {String}
* 返回: {String}

读出已经排队但尚未发送到客户端的消息头。
注意，名称不区分大小写。

例子：

```js
var contentType = response.getHeader('content-type');
```

