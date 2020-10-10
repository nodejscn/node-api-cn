<!-- YAML
added: v0.1.92
changes:
  - version: v12.8.0
    pr-url: https://github.com/nodejs/node/pull/28805
    description: The `outputLength` option was added for XOF hash functions.
-->

* `algorithm` {string}
* `options` {Object} [`stream.transform` 的选项][`stream.transform` options]。
* 返回: {Hash}

创建并返回一个 `Hash` 对象，该对象可用于生成哈希摘要（使用给定的 `algorithm`）。 
可选的 `options` 参数控制流的行为。 
对于 XOF 哈希函数（例如 `'shake256'`），`outputLength` 选项可用于指定所需的输出长度（以字节为单位）。

`algorithm` 取决于平台上的 OpenSSL 的版本所支持的可用算法。 
例如 `'sha256'`、`'sha512'` 等。
在 OpenSSL 的最新版本中，`openssl list -digest-algorithms`（在较旧版本的 OpenSSL 中是 `openssl list-message-digest-algorithms`）将会显示可用的摘要算法。

示例，生成一个文件的 sha256 总和：

```js
const filename = process.argv[2];
const crypto = require('crypto');
const fs = require('fs');

const hash = crypto.createHash('sha256');

const input = fs.createReadStream(filename);
input.on('readable', () => {
  // 哈希流只会生成一个元素。
  const data = input.read();
  if (data)
    hash.update(data);
  else {
    console.log(`${hash.digest('hex')} ${filename}`);
  }
});
```

