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
API usability issues that can lead to accidental security issues.

As an alternative, use one of the following methods of constructing `Buffer`
objects:

* [`Buffer.alloc(size[, fill[, encoding]])`][alloc]: Create a `Buffer` with
  *initialized* memory.
* [`Buffer.allocUnsafe(size)`][alloc_unsafe_size]: Create a `Buffer` with
  *uninitialized* memory.
* [`Buffer.allocUnsafeSlow(size)`][]: Create a `Buffer` with *uninitialized*
   memory.
* [`Buffer.from(array)`][]: Create a `Buffer` with a copy of `array`
* [`Buffer.from(arrayBuffer[, byteOffset[, length]])`][from_arraybuffer] -
  Create a `Buffer` that wraps the given `arrayBuffer`.
* [`Buffer.from(buffer)`][]: Create a `Buffer` that copies `buffer`.
* [`Buffer.from(string[, encoding])`][from_string_encoding]: Create a `Buffer`
  that copies `string`.

Without `--pending-deprecation`, runtime warnings occur only for code not in
`node_modules`. This means there will not be deprecation warnings for
`Buffer()` usage in dependencies. With `--pending-deprecation`, a runtime
warning results no matter where the `Buffer()` usage occurs.

<a id="DEP0006"></a>
