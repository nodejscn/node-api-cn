<!-- YAML
added: v7.7.0
-->

* 返回: {string[]}

返回一个数组，其中包含当前传出的响应头的唯一名称。 
所有响应头名称都是小写的。

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headerNames = response.getHeaderNames();
// headerNames === ['foo', 'set-cookie']
```

