
以下举例说明了一个使用核心 API 的简单的 HTTP/2 服务器。 
由于没有已知的浏览器支持[未加密的 HTTP/2][HTTP/2 Unencrypted]，因此在与浏览器客户端进行通信时必须使用 [`http2.createSecureServer()`]。

```js
const http2 = require('http2');
const fs = require('fs');

const server = http2.createSecureServer({
  key: fs.readFileSync('密钥.pem'),
  cert: fs.readFileSync('证书.pem')
});
server.on('error', (err) => console.error(err));

server.on('stream', (stream, headers) => {
  // 流是一个双工流。
  stream.respond({
    'content-type': 'text/html',
    ':status': 200
  });
  stream.end('<h1>你好世界</h1>');
});

server.listen(8443);
```

要生成此示例的证书和密钥，可以运行：

```bash
openssl req -x509 -newkey rsa:2048 -nodes -sha256 -subj '/CN=localhost' \
  -keyout 密钥.pem -out 证书.pem
```

