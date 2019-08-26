<!-- YAML
added: v9.0.0
-->
* `spkac` {Buffer | TypedArray | DataView}
* 返回 {boolean} 如果 `spkac` 数据结构是有效的返回 `true`，否则返回 `false`。

```js
const { Certificate } = require('crypto');
const spkac = getSpkacSomehow();
console.log(Certificate.verifySpkac(Buffer.from(spkac)));
// 打印 true 或 false。
```
