<!-- YAML
added: v7.7.0
-->

* `name` {string}
* Returns: {boolean}

如果响应头当前有设置 `name` 头部，返回 `true`。请注意，名称匹配不区分大小写。

例子：

```js
const hasContentType = response.hasHeader('content-type');
```

