<!-- YAML
added: v10.0.0
-->

服务器发送 `1xx` 响应时触发（不包括 `101 Upgrade`）。 
使用包含具有状态码的对象的回调触发此事件。

```js
const http = require('http');

const options = {
  host: '127.0.0.1',
  port: 8080,
  path: '/length_request'
};

// 发出请求。
const req = http.request(options);
req.end();

req.on('information', (res) => {
  console.log(`获得主响应之前的信息: ${res.statusCode}`);
});
```

`101 Upgrade` 状态不会触发此事件，因为它们与传统的 HTTP 请求/响应链断开，例如 Web 套接字、现场 TLS 升级、或 HTTP 2.0。 
要收到 `101 Upgrade` 的通知，请改为监听 [`'upgrade'`] 事件。


