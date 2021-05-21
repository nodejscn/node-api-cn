<!-- YAML
added: v0.11.8
-->

* `spkac` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* `encoding` {string} The [encoding][] of the `spkac` string.
* 返回 {boolean} 如果 `spkac` 数据结构是有效的返回 `true`，否则返回 `false`。

```mjs
const { Certificate } = await import('crypto');
const cert = Certificate();
const spkac = getSpkacSomehow();
console.log(cert.verifySpkac(Buffer.from(spkac)));
// Prints: true or false
```

```cjs
const { Certificate } = require('crypto');
const cert = Certificate();
const spkac = getSpkacSomehow();
console.log(cert.verifySpkac(Buffer.from(spkac)));
// Prints: true or false
```

