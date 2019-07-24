<!-- YAML
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Buffer.allocUnsafeSlow()`][] instead.

* `size` {integer} The desired length of the new `SlowBuffer`.

Allocates a new `Buffer` of `size` bytes. If `size` is larger than
[`buffer.constants.MAX_LENGTH`][] or smaller than 0, [`ERR_INVALID_OPT_VALUE`][]
is thrown. A zero-length `Buffer` is created if `size` is 0.

The underlying memory for `SlowBuffer` instances is *not initialized*. The
contents of a newly created `SlowBuffer` are unknown and may contain sensitive
data. Use [`buf.fill(0)`][`buf.fill()`] to initialize a `SlowBuffer` with
zeroes.

```js
const { SlowBuffer } = require('buffer');

const buf = new SlowBuffer(5);

console.log(buf);
// Prints: (contents may vary): <Buffer 78 e0 82 02 01>

buf.fill(0);

console.log(buf);
// Prints: <Buffer 00 00 00 00 00>
```

