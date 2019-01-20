<!-- YAML
added: v7.7.0
-->

* 返回: {Object}

返回当前传出的响应头的浅拷贝。 
由于使用浅拷贝，因此可以更改数组的值而无需额外调用各种与响应头相关的 http 模块方法。 
返回对象的键是响应头名称，值是各自的响应头值。 
所有响应头名称都是小写的。

`response.getHeaders()` 方法返回的对象不是从 JavaScript `Object` 原型继承的。 
这意味着典型的 `Object` 方法，如 `obj.toString()`、`obj.hasOwnProperty()` 等都没有定义并且不起作用。

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headers = response.getHeaders();
// headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
```

