<!-- YAML
added: v0.4.0
-->

* `name` {String}
* `value` {String}

为隐式消息头集合设置一个的消息头值。
如果该消息头已经存在将要发送的消息头集合中，则该值会被覆盖。
如果需要发送多个名称相同的消息头，则使用一个字符串数组。

例子：

```js
response.setHeader('Content-Type', 'text/html');
```

或

```js
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

试图设置一个包含无效字符的消息头字段名称或值会导致抛出一个 [`TypeError`]。

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

