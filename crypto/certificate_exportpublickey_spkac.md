<!-- YAML
added: v0.11.8
-->
- `spkac` {string | Buffer | TypedArray | DataView}
- 返回 {Buffer} 数据结构的公钥部分，`spkac` 包含一个公钥和一个 challange。

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const publicKey = cert.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```
