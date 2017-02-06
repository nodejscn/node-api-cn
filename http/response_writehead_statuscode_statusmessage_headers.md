<!-- YAML
added: v0.1.30
-->

* `statusCode` {Number}
* `statusMessage` {String}
* `headers` {Object}

发送一个响应头给请求。
状态码是一个 3 个数字的 HTTP 状态代码，如 `404`。
最后一个参数 `headers` 是响应头。
第二个参数 `statusMessage` 是可选的。

例子：

```js
var body = 'hello world';
response.writeHead(200, {
  'Content-Length': Buffer.byteLength(body),
  'Content-Type': 'text/plain' });
```

该方法在消息中只能被调用一次，且必须在 [`response.end()`] 被调用之前调用。

如果在调用该方法之前调用 [`response.write()`] 或 [`response.end()`]，则隐式或可变的消息头会被计算并调用该函数。

当消息头已使用 [`response.setHeader()`] 设置，它们会被与其他消息头合并传给 [`response.writeHead()`]，带消息头的 [`response.writeHead()`] 有更高优先级。

```js
// 返回 content-type = text/plain
const server = http.createServer((req,res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('ok');
});
```

注意，`Content-Length` 是以字节（而不是字符）为单位给出的。
以上的例子有效是因为字符串 `'hello world'` 仅包含单字节字符。
如果主体包含更高编码的字符，则 `Buffer.byteLength()` 应被用来确定在给定编码中的字节数。
Node.js 不会检查 `Content-Length` 与已发送的主体长度是否相同。

试图设置一个包含无效字符的消息头字段名称或值会导致抛出一个 [`TypeError`]。

