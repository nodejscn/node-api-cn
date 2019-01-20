<!-- YAML
added: v7.7.0
-->

* `name` {string}
* 返回: {boolean}

如果当前在传出的响应头中设置了由 `name` 标识的响应头，则返回 `true`。 
请注意，响应头名称匹配不区分大小写。

```js
const hasContentType = response.hasHeader('content-type');
```

