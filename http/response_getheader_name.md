<!-- YAML
added: v0.4.0
-->

* `name` {String}
* 返回: {String}

读取一个已入队列但尚未发送到客户端的响应头。
注意，名称不区分大小写。

例子：

```js
var contentType = response.getHeader('content-type');
```

