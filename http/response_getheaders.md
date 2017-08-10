<!-- YAML
added: v7.7.0
-->

* Returns: {Object}

返回当前响应头文件的浅拷贝。 由于使用了浅拷贝，因此数组值可能会改变，无需对各种与响应头相关的http模块方法进行额外调用。
返回对象的键是响应头名称，值是各自的响应头值。 所有响应头名称都是小写的。

注意：`response.getHeaders()` 方法返回的对象不会原型继承 JavaScript `Object`。 这意味着，没有定义典型的Object方法，如`obj.toString()`，`obj.hasOwnProperty()` 和其他方法，并且不起作用。


例子：

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headers = response.getHeaders();
// headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
```

