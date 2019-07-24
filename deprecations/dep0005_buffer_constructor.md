<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19524
    description: Runtime deprecation.
  - version: v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4682
    description: Documentation-only deprecation.
-->

Type: Runtime (supports [`--pending-deprecation`][])

The `Buffer()` function and `new Buffer()` constructor are deprecated due to
API usability issues that can potentially lead to accidental security issues.

As an alternative, use of the following methods of constructing `Buffer` objects
is strongly recommended:

* [`Buffer.alloc(size[, fill[, encoding]])`][alloc] - Create a `Buffer` with
  *initialized* memory.
* [`Buffer.allocUnsafe(size)`][alloc_unsafe_size] - Create a `Buffer` with
  *uninitialized* memory.
* [`Buffer.allocUnsafeSlow(size)`][] - Create a `Buffer` with *uninitialized*
   memory.
* [`Buffer.from(array)`][] - Create a `Buffer` with a copy of `array`
* [`Buffer.from(arrayBuffer[, byteOffset[, length]])`][from_arraybuffer] -
  Create a `Buffer` that wraps the given `arrayBuffer`.
* [`Buffer.from(buffer)`][] - Create a `Buffer` that copies `buffer`.
* [`Buffer.from(string[, encoding])`][from_string_encoding] - Create a `Buffer`
  that copies `string`.

As of v10.0.0, a deprecation warning is printed at runtime when
`--pending-deprecation` is used or when the calling code is
outside `node_modules` in order to better target developers, rather than users.

<a id="DEP0006"></a>
