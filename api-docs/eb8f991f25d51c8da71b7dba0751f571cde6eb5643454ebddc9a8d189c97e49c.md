<!-- YAML
added: v0.11.12
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12223
    description: The `prime` argument can be any `TypedArray` or `DataView` now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11983
    description: The `prime` argument can be a `Uint8Array` now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default for the encoding parameters changed
                 from `binary` to `utf8`.
-->
* `prime` {string | Buffer | TypedArray | DataView}
* `primeEncoding` {string} The [encoding][] of the `prime` string.
* `generator` {number | string | Buffer | TypedArray | DataView} **Default:**
  `2`
* `generatorEncoding` {string} The [encoding][] of the `generator` string.
* Returns: {DiffieHellman}

Creates a `DiffieHellman` key exchange object using the supplied `prime` and an
optional specific `generator`.

The `generator` argument can be a number, string, or [`Buffer`][]. If
`generator` is not specified, the value `2` is used.

If `primeEncoding` is specified, `prime` is expected to be a string; otherwise
a [`Buffer`][], `TypedArray`, or `DataView` is expected.

If `generatorEncoding` is specified, `generator` is expected to be a string;
otherwise a number, [`Buffer`][], `TypedArray`, or `DataView` is expected.

