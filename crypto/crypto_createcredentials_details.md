<!-- YAML
added: v0.1.92
deprecated: v0.11.13
-->

> Stability: 0 - Deprecated: Use [`tls.createSecureContext()`][] instead.

The `crypto.createCredentials()` method is a deprecated alias for creating
and returning a `tls.SecureContext` object. The `crypto.createCredentials()`
method should not be used.

The optional `details` argument is a hash object with keys:

* `pfx` : {String|Buffer} - PFX or PKCS12 encoded private
  key, certificate and CA certificates
* `key` : {String} - PEM encoded private key
* `passphrase` : {String} - passphrase for the private key or PFX
* `cert` : {String} - PEM encoded certificate
* `ca` : {String|Array} - Either a string or array of strings of PEM encoded CA
  certificates to trust.
* `crl` : {String|Array} - Either a string or array of strings of PEM encoded CRLs
  (Certificate Revocation List)
* `ciphers`: {String} using the [OpenSSL cipher list format][] describing the
  cipher algorithms to use or exclude.

If no 'ca' details are given, Node.js will use Mozilla's default
[publicly trusted list of CAs][].

