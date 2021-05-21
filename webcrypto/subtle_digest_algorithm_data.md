<!-- YAML
added: v15.0.0
-->

* `algorithm`: {string|Object}
* `data`: {ArrayBuffer|TypedArray|DataView|Buffer}
* Returns: {Promise} containing {ArrayBuffer}

Using the method identified by `algorithm`, `subtle.digest()` attempts to
generate a digest of `data`. If successful, the returned promise is resolved
with an {ArrayBuffer} containing the computed digest.

If `algorithm` is provided as a {string}, it must be one of:

* `'SHA-1'`
* `'SHA-256'`
* `'SHA-384'`
* `'SHA-512'`

If `algorithm` is provided as an {Object}, it must have a `name` property
whose value is one of the above.

