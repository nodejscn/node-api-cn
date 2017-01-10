<!-- YAML
added: v0.1.92
-->

Verifies the provided data using the given `object` and `signature`.
The `object` argument is a string containing a PEM encoded object, which can be
one an RSA public key, a DSA public key, or an X.509 certificate.
The `signature` argument is the previously calculated signature for the data, in
the `signature_format` which can be `'latin1'`, `'hex'` or `'base64'`.
If a `signature_format` is specified, the `signature` is expected to be a
string; otherwise `signature` is expected to be a [`Buffer`][].

Returns `true` or `false` depending on the validity of the signature for
the data and public key.

The `verifier` object can not be used again after `verify.verify()` has been
called. Multiple calls to `verify.verify()` will result in an error being
thrown.

