<!-- YAML
added: v7.7.0
-->

* `name` {string}
* 返回: {boolean}

如果响应头有设置 `name` 响应头，则返回 `true`。
响应头名称匹配不区分大小写。

例子：

```js
const hasContentType = response.hasHeader('content-type');
```

