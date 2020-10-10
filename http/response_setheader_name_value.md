<!-- YAML
added: v0.4.0
-->

* `name` {string}
* `value` {any}

为隐式响应头设置单个响应头的值。
如果此响应头已存在于待发送的响应头中，则其值将被替换。
在这里可以使用字符串数组来发送具有相同名称的多个响应头。
非字符串值将被原样保存。
因此 [`response.getHeader()`] 可能返回非字符串值。
但是非字符串值将转换为字符串以进行网络传输。

```js
response.setHeader('Content-Type', 'text/html');
```

或：

```js
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

尝试设置包含无效字符的响应头字段名称或值将导致抛出 [`TypeError`]。

当使用 [`response.setHeader()`] 设置响应头时，它们将与传给 [`response.writeHead()`] 的任何响应头合并，其中 [`response.writeHead()`] 的响应头优先。

```js
// 返回 content-type = text/plain
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

如果调用了 [`response.writeHead()`] 方法并且尚未调用此方法，则它将直接将提供的响应头值写入网络通道而不在内部进行缓存，并且响应头上的 [`response.getHeader()`] 将不会产生预期的结果。
如果需要渐进的响应头填充以及将来可能的检索和修改，则使用 [`response.setHeader()`] 而不是 [`response.writeHead()`]。

