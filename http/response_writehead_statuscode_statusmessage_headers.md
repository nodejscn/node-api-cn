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

发送一个响应头给请求。
状态码是一个三位数的 HTTP 状态码，如 `404`。
最后一个参数 `headers` 是响应头。
第二个参数 `statusMessage` 是可选的状态描述。

例子：

```js
const body = 'hello world';
response.writeHead(200, {
  'Content-Length': Buffer.byteLength(body),
  'Content-Type': 'text/plain' });
```

该方法在消息中只能被调用一次，且必须在 [`response.end()`] 被调用之前调用。

如果在调用该方法之前调用 [`response.write()`] 或 [`response.end()`]，则隐式的响应头会被处理并调用该函数。

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

注意，`Content-Length` 是以字节（而不是字符）为单位的。
上面的例子行得通是因为字符串 `'hello world'` 只包含单字节字符。
如果响应主体包含高级编码的字符，则应使用 `Buffer.byteLength()` 来确定在给定编码中的字节数。
Node.js 不会检查 `Content-Length` 与已发送的响应主体的长度是否相同。

如果响应头字段的名称或值包含无效字符，则抛出 [`TypeError`] 错误。

