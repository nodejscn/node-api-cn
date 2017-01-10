<!-- YAML
added: v0.11.13
-->

* `options` {Object}
  * `pfx` {string|Buffer} A string or `Buffer` holding the PFX or PKCS12 encoded
    private key, certificate, and CA certificates.
  * `key` {string|string[]|Buffer|Object[]} The private key of the server in
    PEM format. To support multiple keys using different algorithms, an array
    can be provided either as an array of key strings or as an array of objects
    in the format `{pem: key, passphrase: passphrase}`. This option is
    *required* for ciphers that make use of private keys.
  * `passphrase` {string} A string containing the passphrase for the private key
    or pfx.
  * `cert` {string} A string containing the PEM encoded certificate
  * `ca`{string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of strings,
    or array of `Buffer`s of trusted certificates in PEM format. If omitted,
    several well known "root" CAs (like VeriSign) will be used. These are used
    to authorize connections.
  * `crl` {string|string[]} Either a string or array of strings of PEM encoded
    CRLs (Certificate Revocation List).
  * `ciphers` {string} A string describing the ciphers to use or exclude.
    Consult
    <https://www.openssl.org/docs/man1.0.2/apps/ciphers.html#CIPHER-LIST-FORMAT>
    for details on the format.
  * `honorCipherOrder` {boolean} If `true`, when a cipher is being selected,
    the server's preferences will be used instead of the client preferences.

The `tls.createSecureContext()` method creates a credentials object.

If the 'ca' option is not given, then Node.js will use the default
publicly trusted list of CAs as given in
<http://mxr.mozilla.org/mozilla/source/security/nss/lib/ckfw/builtins/certdata.txt>.


