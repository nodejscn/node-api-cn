<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.allocUnsafeSlow()`] 代替。

* `size` {integer} The desired length of the new `SlowBuffer`

Allocates a new `Buffer` of `size` bytes.  If the `size` is larger than
[`buffer.kMaxLength`] or smaller than 0, a [`RangeError`] will be thrown.
A zero-length `Buffer` will be created if `size` is 0.

The underlying memory for `SlowBuffer` instances is *not initialized*. The
contents of a newly created `SlowBuffer` are unknown and could contain
sensitive data. Use [`buf.fill(0)`][`buf.fill()`] to initialize a `SlowBuffer` to zeroes.

Example:

```js
const { SlowBuffer } = require('buffer');

const buf = new SlowBuffer(5);

// Prints: (contents may vary): <Buffer 78 e0 82 02 01>
console.log(buf);

buf.fill(0);

// Prints: <Buffer 00 00 00 00 00>
console.log(buf);
```

