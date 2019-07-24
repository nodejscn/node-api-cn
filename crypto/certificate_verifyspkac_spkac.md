<!-- YAML
added: v0.11.8
-->
- `spkac` {Buffer | TypedArray | DataView}
- 返回 {boolean} 如果 `spkac` 数据结构是有效的返回 `true`，否则返回 `false`。

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
console.log(cert.verifySpkac(Buffer.from(spkac)));
// Prints: true 或者 false
```
