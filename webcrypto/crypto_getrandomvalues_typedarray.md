<!-- YAML
added: v15.0.0
-->

* `typedArray` {Buffer|TypedArray|DataView|ArrayBuffer}
* Returns: {Buffer|TypedArray|DataView|ArrayBuffer} Returns `typedArray`.

Generates cryptographically strong random values. The given `typedArray` is
filled with random values, and a reference to `typedArray` is returned.

An error will be thrown if the given `typedArray` is larger than 65,536 bytes.

