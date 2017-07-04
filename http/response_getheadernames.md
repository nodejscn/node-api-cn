<!-- YAML
added: v7.7.0
-->

* Returns: {Array}

返回一个包含当前响应唯一名称的 http 头信息名称数组. 名称均为小写.

示例:

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headerNames = response.getHeaderNames();
// headerNames === ['foo', 'set-cookie']
```

