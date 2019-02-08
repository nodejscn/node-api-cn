<!-- YAML
added: v0.1.30
changes:
  - version: v5.11.0, v4.4.5
    pr-url: https://github.com/nodejs/node/pull/6291
    description: A `RangeError` is thrown if `statusCode` is not a number in
                 the range `[100, 999]`.
-->

* `statusCode` {number}
* `statusMessage` {string}
* `headers` {Object}

向请求发送响应头。
状态码是一个 3 位的 HTTP 状态码，如 `404`。
最后一个参数 `headers` 是响应头。
可以可选地将用户可读的 `statusMessage` 作为第二个参数。

```js
const body = 'hello world';
response.writeHead(200, {
  'Content-Length': Buffer.byteLength(body),
  'Content-Type': 'text/plain' });
```

此方法只能在消息上调用一次，并且必须在调用 [`response.end()`] 之前调用。

如果在调用此方法之前调用了 [`response.write()`] 或 [`response.end()`]，则将计算隐式或可变的响应头并调用此函数。

当使用 [`response.setHeader()`] 设置响应头时，则与传给 [`response.writeHead()`] 的任何响应头合并，且 [`response.writeHead()`] 的优先。

如果调用此方法并且尚未调用 [`response.setHeader()`]，则直接将提供的响应头值写入网络通道而不在内部进行缓存，响应头上的 [`response.getHeader()`] 将不会产生预期的结果。
如果需要渐进的响应头填充以及将来可能的检索和修改，则改用 [`response.setHeader()`]。

```js
// 返回 content-type = text/plain
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

注意，Content-Length 以字节而非字符为单位。
上面的示例可行是因为字符串 `'hello world'` 仅包含单字节字符。
如果主体包含更高编码的字符，则应使用 `Buffer.byteLength()` 来判断给定编码中的字节数。
Node.js 不检查 Content-Length 和已传输的主体的长度是否相等。

尝试设置包含无效字符的响应头字段名称或值将导致抛出 [`TypeError`]。

