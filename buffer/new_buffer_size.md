<!-- YAML
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Buffer.alloc()`] instead (also see
> [`Buffer.allocUnsafe()`]).

* `size` {Integer} The desired length of the new `Buffer`

Allocates a new `Buffer` of `size` bytes.  The `size` must be less than or equal
to the value of [`buffer.kMaxLength`]. Otherwise, a [`RangeError`] is thrown.
A zero-length `Buffer` will be created if `size <= 0`.

Unlike [`ArrayBuffers`][`ArrayBuffer`], the underlying memory for `Buffer` instances
created in this way is *not initialized*. The contents of a newly created `Buffer`
are unknown and *could contain sensitive data*. Use
[`Buffer.alloc(size)`][`Buffer.alloc()`] instead to initialize a `Buffer` to zeroes.

Example:

```js
const buf = new Buffer(5);

// Prints: (contents may vary): <Buffer 78 e0 82 02 01>
console.log(buf);

buf.fill(0);

// Prints: <Buffer 00 00 00 00 00>
console.log(buf);
```

