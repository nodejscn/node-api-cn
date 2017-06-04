
Type: Documentation-only

The `Buffer()` function and `new Buffer()` constructor are deprecated due to
API usability issues that can potentially lead to accidental security issues.

As an alternative, use of the following methods of constructing `Buffer` objects
is strongly recommended:

* [`Buffer.alloc(size[, fill[, encoding]])`][alloc] - Create a `Buffer` with
  *initialized* memory.
* [`Buffer.allocUnsafe(size)`][alloc_unsafe_size] - Create a `Buffer` with *uninitialized*
  memory.
* [`Buffer.allocUnsafeSlow(size)`][] - Create a `Buffer` with *uninitialized*
   memory.
* [`Buffer.from(array)`][] - Create a `Buffer` with a copy of `array`
* [`Buffer.from(arrayBuffer[, byteOffset[, length]])`][from_arraybuffer] - Create a `Buffer`
  that wraps the given `arrayBuffer`.
* [`Buffer.from(buffer)`][] - Create a `Buffer` that copies `buffer`.
* [`Buffer.from(string[, encoding])`][from_string_encoding] - Create a `Buffer` that copies
  `string`.

<a id="DEP0006"></a>
