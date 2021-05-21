<!-- YAML
added: v15.7.0
-->

* `sources` {string[]|ArrayBuffer[]|TypedArray[]|DataView[]|Blob[]} An array
  of string, {ArrayBuffer}, {TypedArray}, {DataView}, or {Blob} objects, or
  any mix of such objects, that will be stored within the `Blob`.
* `options` {Object}
  * `encoding` {string} The character encoding to use for string sources.
    **Default:** `'utf8'`.
  * `type` {string} The Blob content-type. The intent is for `type` to convey
    the MIME media type of the data, however no validation of the type format
    is performed.

Creates a new `Blob` object containing a concatenation of the given sources.

{ArrayBuffer}, {TypedArray}, {DataView}, and {Buffer} sources are copied into
the 'Blob' and can therefore be safely modified after the 'Blob' is created.

String sources are also copied into the `Blob`.

