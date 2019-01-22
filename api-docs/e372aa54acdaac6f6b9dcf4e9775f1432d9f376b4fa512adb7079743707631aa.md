<!-- YAML
added: v0.3.0
-->

* {boolean}

如果已收到并成功解析完整的 HTTP 消息，则 `message.complete` 属性将为 `true`。

此属性可用于判断客户端或服务器在连接终止之前是否完全传输消息：

```js
const req = http.request({
  host: '127.0.0.1',
  port: 8080,
  method: 'POST'
}, (res) => {
  res.resume();
  res.on('end', () => {
    if (!res.complete)
      console.error(
        '消息仍在发送时终止了连接');
  });
});
```

