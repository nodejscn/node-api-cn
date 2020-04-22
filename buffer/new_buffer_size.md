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

See [`Buffer.alloc()`][] and [`Buffer.allocUnsafe()`][]. This variant of the
constructor is equivalent to [`Buffer.allocUnsafe()`][], although using
[`Buffer.alloc()`][] is recommended in code paths that are not critical to
performance.

