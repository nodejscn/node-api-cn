<!-- YAML
added: v0.1.94
changes:
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: The `key` argument can now be a `KeyObject`.
-->

* `algorithm` {string}
* `key` {string | Buffer | TypedArray | DataView | KeyObject}
* `options` {Object} [`stream.transform` 的选项][`stream.transform` options]。
* 返回: {Hmac}

创建并返回一个 `Hmac` 对象，该对象使用给定的 `algorithm` 和 `key`。 
可选的 `options` 参数控制流的行为。 

`algorithm` 取决于平台上的 OpenSSL 的版本所支持的可用算法。 
例如 `'sha256'`、`'sha512'` 等。
在 OpenSSL 的最新版本中，`openssl list -digest-algorithms`（在较旧版本的 OpenSSL 中是 `openssl list-message-digest-algorithms`）将会显示可用的摘要算法。

`key` 是用于生成加密的 HMAC 哈希的 HMAC 密钥。 
如果它是一个 [`KeyObject`]，则其类型必须是 `secret`。

示例，生成一个文件的 sha256 HMAC：

```js
const filename = process.argv[2];
const crypto = require('crypto');
const fs = require('fs');

const hmac = crypto.createHmac('sha256', '密钥');

const input = fs.createReadStream(filename);
input.on('readable', () => {
  // 哈希流只会生成一个元素。
  const data = input.read();
  if (data)
    hmac.update(data);
  else {
    console.log(`${hmac.digest('hex')} ${filename}`);
  }
});
```

