<!-- YAML
added: v9.0.0
-->
* `spkac` {string | Buffer | TypedArray | DataView}
* 返回 {Buffer} 返回 `spkac` 数据结构的 challenge 部分，`spkac` 包含一个公钥和一个 challange。

```js
const { Certificate } = require('crypto');
const spkac = getSpkacSomehow();
const challenge = Certificate.exportChallenge(spkac);
console.log(challenge.toString('utf8'));
// 以 UTF 字符串的形式打印 challenge。
```
