<!-- YAML
added: v0.1.92
-->

Calculates the signature on all the data passed through using either
[`sign.update()`][] or [`sign.write()`][stream-writable-write].

The `private_key` argument can be an object or a string. If `private_key` is a
string, it is treated as a raw key with no passphrase. If `private_key` is an
object, it is interpreted as a hash containing two properties:

* `key` : {String} - PEM encoded private key
* `passphrase` : {String} - passphrase for the private key

The `output_format` can specify one of `'latin1'`, `'hex'` or `'base64'`. If
`output_format` is provided a string is returned; otherwise a [`Buffer`][] is
returned.

The `Sign` object can not be again used after `sign.sign()` method has been
called. Multiple calls to `sign.sign()` will result in an error being thrown.

