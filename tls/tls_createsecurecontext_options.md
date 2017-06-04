<!-- YAML
added: v0.11.13
changes:
  - version: v7.3.0
    pr-url: https://github.com/nodejs/node/pull/10294
    description: If the `key` option is an array, individual entries do not
                 need a `passphrase` property anymore. Array entries can also
                 just be `string`s or `Buffer`s now.
  - version: v5.2.0
    pr-url: https://github.com/nodejs/node/pull/4099
    description: The `ca` option can now be a single string containing multiple
                 CA certificates.
-->

* `options` {Object}
  * `pfx` {string|Buffer} Optional PFX or PKCS12 encoded private key and
    certificate chain. `pfx` is an alternative to providing `key` and `cert`
    individually. PFX is usually encrypted, if it is, `passphrase` will be used
    to decrypt it.
  * `key` {string|string[]|Buffer|Buffer[]|Object[]} Optional private keys in
    PEM format. PEM allows the option of private keys being encrypted. Encrypted
    keys will be decrypted with `options.passphrase`.  Multiple keys using
    different algorithms can be provided either as an array of unencrypted key
    strings or buffers, or an array of objects in the form `{pem:
    <string|buffer>[, passphrase: <string>]}`. The object form can only occur in
    an array. `object.passphrase` is optional. Encrypted keys will be decrypted
    with `object.passphrase` if provided, or `options.passphrase` if it is not.
  * `passphrase` {string} Optional shared passphrase used for a single private
    key and/or a PFX.
  * `cert` {string|string[]|Buffer|Buffer[]} Optional cert chains in PEM format.
    One cert chain should be provided per private key. Each cert chain should
    consist of the PEM formatted certificate for a provided private `key`,
    followed by the PEM formatted intermediate certificates (if any), in order,
    and not including the root CA (the root CA must be pre-known to the peer,
    see `ca`).  When providing multiple cert chains, they do not have to be in
    the same order as their private keys in `key`. If the intermediate
    certificates are not provided, the peer will not be able to validate the
    certificate, and the handshake will fail.
  * `ca` {string|string[]|Buffer|Buffer[]} Optionally override the trusted CA
    certificates. Default is to trust the well-known CAs curated by Mozilla.
    Mozilla's CAs are completely replaced when CAs are explicitly specified
    using this option. The value can be a string or Buffer, or an Array of
    strings and/or Buffers. Any string or Buffer can contain multiple PEM CAs
    concatenated together. The peer's certificate must be chainable to a CA
    trusted by the server for the connection to be authenticated.  When using
    certificates that are not chainable to a well-known CA, the certificate's CA
    must be explicitly specified as a trusted or the connection will fail to
    authenticate.
    If the peer uses a certificate that doesn't match or chain to one of the
    default CAs, use the `ca` option to provide a CA certificate that the peer's
    certificate can match or chain to.
    For self-signed certificates, the certificate is its own CA, and must be
    provided.
  * `crl` {string|string[]|Buffer|Buffer[]} Optional PEM formatted
    CRLs (Certificate Revocation Lists).
  * `ciphers` {string} Optional cipher suite specification, replacing the
    default.  For more information, see [modifying the default cipher suite][].
  * `honorCipherOrder` {boolean} Attempt to use the server's cipher suite
    preferences instead of the client's. When `true`, causes
    `SSL_OP_CIPHER_SERVER_PREFERENCE` to be set in `secureOptions`, see
    [OpenSSL Options][] for more information.
  * `ecdhCurve` {string} A string describing a named curve to use for ECDH key
    agreement or `false` to disable ECDH. Defaults to
    [`tls.DEFAULT_ECDH_CURVE`].  Use [`crypto.getCurves()`][] to obtain a list
    of available curve names. On recent releases, `openssl ecparam -list_curves`
    will also display the name and description of each available elliptic curve.
  * `dhparam` {string|Buffer} Diffie Hellman parameters, required for
    [Perfect Forward Secrecy][]. Use `openssl dhparam` to create the parameters.
    The key length must be greater than or equal to 1024 bits, otherwise an
    error will be thrown. It is strongly recommended to use 2048 bits or larger
    for stronger security. If omitted or invalid, the parameters are silently
    discarded and DHE ciphers will not be available.
  * `secureProtocol` {string} Optional SSL method to use, default is
    `"SSLv23_method"`. The possible values are listed as [SSL_METHODS][], use
    the function names as strings. For example, `"SSLv3_method"` to force SSL
    version 3.
  * `secureOptions` {number} Optionally affect the OpenSSL protocol behavior,
    which is not usually necessary. This should be used carefully if at all!
    Value is a numeric bitmask of the `SSL_OP_*` options from
    [OpenSSL Options][].
  * `sessionIdContext` {string} Optional opaque identifier used by servers to
    ensure session state is not shared between applications. Unused by clients.

*Note*:

* [`tls.createServer()`][] sets the default value of the
  `honorCipherOrder` option to `true`, other APIs that create secure contexts
  leave it unset.

* [`tls.createServer()`][] uses a 128 bit truncated SHA1 hash value
  generated from `process.argv` as the default value of the `sessionIdContext`
  option, other APIs that create secure contexts have no default value.

The `tls.createSecureContext()` method creates a credentials object.

A key is *required* for ciphers that make use of certificates. Either `key` or
`pfx` can be used to provide it.

If the 'ca' option is not given, then Node.js will use the default
publicly trusted list of CAs as given in
<http://mxr.mozilla.org/mozilla/source/security/nss/lib/ckfw/builtins/certdata.txt>.


