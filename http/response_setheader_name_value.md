<!-- YAML
added: v0.4.0
-->

* `name` {string}
* `value` {any}

为一个隐式的响应头设置值。
如果该响应头已存在，则值会被覆盖。
如果要发送多个名称相同的响应头，则使用字符串数组。
非字符串的值会保留原样，所以 [`response.getHeader()`] 会返回非字符串的值。
非字符串的值在网络传输时会转换为字符串。

例子：

```js
response.setHeader('Content-Type', 'text/html');
```

或：

```js
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

如果响应头字段的名称或值包含无效字符，则抛出 [`TypeError`] 错误。

[`response.setHeader()`] 设置的响应头会与 [`response.writeHead()`] 设置的响应头合并，且 [`response.writeHead()`] 的优先。

```js
// 返回 content-type = text/plain
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

