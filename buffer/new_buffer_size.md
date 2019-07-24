<!-- YAML
deprecated: v6.0.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19524
    description: Calling this constructor emits a deprecation warning when
                 run from code outside the `node_modules` directory.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12141
    description: The `new Buffer(size)` will return zero-filled memory by
                 default.
  - version: v7.2.1
    pr-url: https://github.com/nodejs/node/pull/9529
    description: Calling this constructor no longer emits a deprecation warning.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8169
    description: Calling this constructor emits a deprecation warning now.
-->

> Stability: 0 - Deprecated: Use [`Buffer.alloc()`][] instead (also see
> [`Buffer.allocUnsafe()`][]).

* `size` {integer} The desired length of the new `Buffer`.

Allocates a new `Buffer` of `size` bytes. If `size` is larger than
[`buffer.constants.MAX_LENGTH`][] or smaller than 0, [`ERR_INVALID_OPT_VALUE`][]
is thrown. A zero-length `Buffer` is created if `size` is 0.

Prior to Node.js 8.0.0, the underlying memory for `Buffer` instances
created in this way is *not initialized*. The contents of a newly created
`Buffer` are unknown and *may contain sensitive data*. Use
[`Buffer.alloc(size)`][`Buffer.alloc()`] instead to initialize a `Buffer`
with zeroes.

```js
const buf = new Buffer(10);

console.log(buf);
// Prints: <Buffer 00 00 00 00 00 00 00 00 00 00>
```

