<!-- YAML
added: v10.0.0
-->

在服务器发送 1xx 代号的响应时触发（101 Upgrade 响应除外）。
该事件会调用一个回调函数，其参数是一个存有状态码的对象。

```js
const http = require('http');

const options = {
  hostname: '127.0.0.1',
  port: 8080,
  path: '/length_request'
};

// 发送请求。
const req = http.request(options);
req.end();

req.on('information', (res) => {
  console.log(`在主响应之前获得信息: ${res.statusCode}`);
});
```

101 Upgrade 状态不会触发该事件，因为它们会断开传统的HTTP的请求/响应链，例如改用 Web Socket、现 场TLS 升级、采用 HTTP 2.0。
若要获知 101 Upgrade 通知，请监听 [`'upgrade'`] 事件。

