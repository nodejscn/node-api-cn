<!-- YAML
added: v0.11.8
-->
- `spkac` {string | Buffer | TypedArray | DataView}
- 返回 {Buffer} 返回 `spkac` 数据结构的 challenge 部分，`spkac` 包含一个公钥和一个 challange。

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const challenge = cert.exportChallenge(spkac);
console.log(challenge.toString('utf8'));
// Prints: the challenge as a UTF8 string
```
