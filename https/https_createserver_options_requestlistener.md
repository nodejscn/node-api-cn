<!-- YAML
added: v0.3.4
-->
* `options` {Object} 接受来自 [`tls.createServer()`]、[`tls.createSecureContext()`] 和 [`http.createServer()`] 的 `options`。
* `requestListener` {Function} 要添加到 `'request'` 事件的监听器。
* 返回: {https.Server}

```js
// curl -k https://localhost:8000/
const https = require('https');
const fs = require('fs');

const options = {
  key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
  cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem')
};

https.createServer(options, (req, res) => {
  res.writeHead(200);
  res.end('你好，世界\n');
}).listen(8000);
```

或者：

```js
const https = require('https');
const fs = require('fs');

const options = {
  pfx: fs.readFileSync('test/fixtures/test_cert.pfx'),
  passphrase: '密码'
};

https.createServer(options, (req, res) => {
  res.writeHead(200);
  res.end('你好，世界\n');
}).listen(8000);
```

