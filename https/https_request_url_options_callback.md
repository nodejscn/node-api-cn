<!-- YAML
added: v0.3.6
changes:
  - version: v14.1.0
    pr-url: https://github.com/nodejs/node/pull/32786
    description: The `highWaterMark` option is accepted now.
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: 现在可以将 `url` 参数与一个单独的 `options` 对象一起传入。
  - version: v9.3.0
    pr-url: https://github.com/nodejs/node/pull/14903
    description: 参数 `options` 现在可以包含 `clientCertEngine`。
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: 参数 `options` 可以是 WHATWG `URL` 对象。
-->
* `url` {string | URL}
* `options` {Object | string | URL} 接受来自 [`http.request()`] 的所有 `options`，但默认值有一些差异：
  - `protocol` **默认值:** `'https:'`。
  - `port` **默认值:** `443`。
  - `agent` **默认值:** `https.globalAgent`。
* `callback` {Function}

发送一个请求到一个加密的 Web 服务器。

以下来自 [`tls.connect()`] 的额外的 `options` 也会被接收：
`ca`、`cert`、`ciphers`、`clientCertEngine`、`crl`、`dhparam`、`ecdhCurve`、`honorCipherOrder`、`key`、`passphrase`、`pfx`、`rejectUnauthorized`、`secureOptions`、`secureProtocol`、`servername`、`sessionIdContext`、`highWaterMark`。

`options` 可以是对象、字符串、或 [`URL`] 对象。
如果 `options` 是一个字符串, 则会被自动地使用 [`new URL()`] 解析。
如果是一个 [`URL`] 对象，则会被自动地转换为一个普通的 `options` 对象。

```js
const https = require('https');

const options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET'
};

const req = https.request(options, (res) => {
  console.log('状态码:', res.statusCode);
  console.log('请求头:', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });
});

req.on('error', (e) => {
  console.error(e);
});
req.end();
```

使用 [`tls.connect()`] 的选项的示例：

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

或者，不使用 [`Agent`] 而选择退出连接池。

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

使用 [`URL`] 作为 `options` 的示例：

```js
const options = new URL('https://abc:xyz@example.com');

const req = https.request(options, (res) => {
  // ...
});
```

固定证书指纹或公钥（类似于 `pin-sha256`）的示例：

```js
const tls = require('tls');
const https = require('https');
const crypto = require('crypto');

function sha256(s) {
  return crypto.createHash('sha256').update(s).digest('base64');
}
const options = {
  hostname: 'github.com',
  port: 443,
  path: '/',
  method: 'GET',
  checkServerIdentity: function(host, cert) {
    // 确保将证书颁发给所连接的主机。
    const err = tls.checkServerIdentity(host, cert);
    if (err) {
      return err;
    }

    // 固定公钥，类似于固定的 HPKP pin-sha25。
    const pubkey256 = 'pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=';
    if (sha256(cert.pubkey) !== pubkey256) {
      const msg = '证书验证错误: ' +
        `'${cert.subject.CN}' 的公钥` +
        '与固定的指纹不符';
      return new Error(msg);
    }

    // 固定确切的证书，而不是公钥。
    const cert256 = '25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:' +
      'D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16';
    if (cert.fingerprint256 !== cert256) {
      const msg = '证书验证错误: ' +
        `'${cert.subject.CN}' 的证书` +
        '与固定的指纹不符';
      return new Error(msg);
    }

    // 此循环仅供参考。
    // 打印链条中所有证书的证书与公钥指纹。 
    // 通常，将发行人的公钥固定在公共互联网上，同时将服务的公钥固定在私密的环境中。
    do {
      console.log('主体的常用名称:', cert.subject.CN);
      console.log('  证书的 SHA256 指纹:', cert.fingerprint256);

      hash = crypto.createHash('sha256');
      console.log('  公钥的 ping-sha256:', sha256(cert.pubkey));

      lastprint256 = cert.fingerprint256;
      cert = cert.issuerCertificate;
    } while (cert.fingerprint256 !== lastprint256);

  },
};

options.agent = new https.Agent(options);
const req = https.request(options, (res) => {
  console.log('一切正常。服务器与固定的证书或公钥相匹配。');
  console.log('状态码:', res.statusCode);
  // 打印 HPKP 的值。
  console.log('请求头:', res.headers['public-key-pins']);

  res.on('data', (d) => {});
});

req.on('error', (e) => {
  console.error(e.message);
});
req.end();
```

示例的输出：

```text
主体的常用名称: github.com
  证书的 SHA256 指纹: 25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16
  公钥的 ping-sha256: pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=
主体的常用名称: DigiCert SHA2 Extended Validation Server CA
  证书的 SHA256 指纹: 40:3E:06:2A:26:53:05:91:13:28:5B:AF:80:A0:D4:AE:42:2C:84:8C:9F:78:FA:D0:1F:C9:4B:C5:B8:7F:EF:1A
  公钥的 ping-sha256: RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho=
主体的常用名称: DigiCert High Assurance EV Root CA
  证书的 SHA256 指纹: 74:31:E5:F4:C3:C1:CE:46:90:77:4F:0B:61:E0:54:40:88:3B:A9:A0:1E:D0:0B:A6:AB:D7:80:6E:D3:B1:18:CF
  公钥的 ping-sha256: WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18=
一切正常。服务器与固定的证书或公钥相匹配。
状态码: 200
请求头: max-age=0; pin-sha256="WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18="; pin-sha256="RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho="; pin-sha256="k2v657xBsOVe1PQRwOsHsw3bsGT2VzIqz5K+59sNQws="; pin-sha256="K87oWBWM9UZfyddvDfoxL+8lpNyoUB2ptGtn0fv6G2Q="; pin-sha256="IQBnNBEiFuhj+8x6X8XLgh01V9Ic5/V3IRQLNFFc7v4="; pin-sha256="iie1VXtL7HzAMF+/PVPR9xzT80kQxdZeJ+zduCB3uj0="; pin-sha256="LvRiGEjRqfzurezaWuj8Wie2gyHMrW5Q06LspMnox7A="; includeSubDomains
```


