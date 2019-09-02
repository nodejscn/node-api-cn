<!-- YAML
added: v10.0.0
-->

* `info` {Object}
  * `httpVersion` {string}
  * `httpVersionMajor` {integer}
  * `httpVersionMinor` {integer}
  * `statusCode` {integer}
  * `statusMessage` {string}
  * `headers` {Object}
  * `rawHeaders` {string[]}


服务器发送 1xx 中间响应（不包括 101 Upgrade）时触发。 
此事件的监听器将会接收一个对象，该对象包含 HTTP 版本，状态码，状态消息，键值对请求头对象、以及具有原始请求头名称和值的数组。

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

req.on('information', (info) => {
  console.log(`获得主响应之前的信息: ${info.statusCode}`);
});
```

`101 Upgrade` 状态不会触发此事件，因为它们与传统的 HTTP 请求/响应链断开，例如 Web 套接字、现场 TLS 升级、或 HTTP 2.0。 
要收到 `101 Upgrade` 的通知，请改为监听 [`'upgrade'`] 事件。


