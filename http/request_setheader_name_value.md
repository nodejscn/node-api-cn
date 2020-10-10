<!-- YAML
added: v1.6.0
-->

* `name` {string}
* `value` {any}

为请求头对象设置单个请求头的值。 
如果此请求头已存在于待发送的请求头中，则其值将被替换。 
这里可以使用字符串数组来发送具有相同名称的多个请求头。 
非字符串值将被原样保存。 
因此 [`request.getHeader()`] 可能会返回非字符串值。 
但是非字符串值将转换为字符串以进行网络传输。

```js
request.setHeader('Content-Type', 'application/json');
```

或：

```js
request.setHeader('Cookie', ['type=ninja', 'language=javascript']);
```

