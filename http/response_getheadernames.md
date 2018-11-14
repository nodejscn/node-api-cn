<!-- YAML
added: v7.7.0
-->

* 返回: {string[]}

返回包含当前响应头名称的数组。
响应头名称均为小写。

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headerNames = response.getHeaderNames();
// headerNames === ['foo', 'set-cookie']
```

