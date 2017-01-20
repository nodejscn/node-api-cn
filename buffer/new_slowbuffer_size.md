<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.allocUnsafeSlow()`] 代替。

* `size` {Integer} The desired length of the new `SlowBuffer`

Allocates a new `SlowBuffer` of `size` bytes. The `size` must be less than
or equal to the value of [`buffer.kMaxLength`]. Otherwise, a [`RangeError`] is
thrown. A zero-length `Buffer` will be created if `size <= 0`.

The underlying memory for `SlowBuffer` instances is *not initialized*. The
contents of a newly created `SlowBuffer` are unknown and could contain
sensitive data. Use [`buf.fill(0)`][`buf.fill()`] to initialize a `SlowBuffer` to zeroes.

Example:

```js
const SlowBuffer = require('buffer').SlowBuffer;

const buf = new SlowBuffer(5);

// Prints: (contents may vary): <Buffer 78 e0 82 02 01>
console.log(buf);

buf.fill(0);

// Prints: <Buffer 00 00 00 00 00>
console.log(buf);
```

