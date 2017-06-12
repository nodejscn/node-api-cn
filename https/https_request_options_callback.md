<!-- YAML
added: v0.3.6
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->
- `options` {Object | string | URL} Accepts all `options` from [`http.request()`][],
  with some differences in default values:
  - `protocol` Defaults to `https:`
  - `port` Defaults to `443`.
  - `agent` Defaults to `https.globalAgent`.
- `callback` {Function}

向一个安全的服务器发起一个请求。

The following additional `options` from [`tls.connect()`][] are also accepted when using a
  custom [`Agent`][]:
  `pfx`, `key`, `passphrase`, `cert`, `ca`, `ciphers`, `rejectUnauthorized`, `secureProtocol`, `servername`

参数 `options` 可以是一个对象、或字符串、或 [`URL`] 对象。
如果参数 `options` 是一个字符串, 它自动被 [`url.parse()`] 所解析。
If it is a [`URL`][] object, it will be automatically converted to an ordinary `options` object.

例子:

```js
const https = require('https');

const options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET'
};

const req = https.request(options, (res) => {
  console.log('状态码：', res.statusCode);
  console.log('请求头：', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });
});

req.on('error', (e) => {
  console.error(e);
});
req.end();
```

Example using options from [`tls.connect()`][]:

```js
const options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET',
  key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
  cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem')
};
options.agent = new https.Agent(options);

const req = https.request(options, (res) => {
  // ...
});
```

也可以不对连接池使用 `Agent`。

例子:

```js
const options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET',
  key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
  cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  agent: false
};

const req = https.request(options, (res) => {
  // ...
});
```

Example using a [`URL`][] as `options`:

```js
const { URL } = require('url');

const options = new URL('https://abc:xyz@example.com');

const req = https.request(options, (res) => {
  // ...
});
```

