<!-- YAML
added: v15.0.0
-->

* `nameOrNid`: {string|number} The name or nid of the cipher to query.
* `options`: {Object}
  * `keyLength`: {number} A test key length.
  * `ivLength`: {number} A test IV length.
* Returns: {Object}
  * `name` {string} The name of the cipher
  * `nid` {number} The nid of the cipher
  * `blockSize` {number} The block size of the cipher in bytes. This property
    is omitted when `mode` is `'stream'`.
  * `ivLength` {number} The expected or default initialization vector length in
    bytes. This property is omitted if the cipher does not use an initialization
    vector.
  * `keyLength` {number} The expected or default key length in bytes.
  * `mode` {string} The cipher mode. One of `'cbc'`, `'ccm'`, `'cfb'`, `'ctr'`,
    `'ecb'`, `'gcm'`, `'ocb'`, `'ofb'`, `'stream'`, `'wrap'`, `'xts'`.

Returns information about a given cipher.

Some ciphers accept variable length keys and initialization vectors. By default,
the `crypto.getCipherInfo()` method will return the default values for these
ciphers. To test if a given key length or iv length is acceptable for given
cipher, use the `keyLength` and `ivLength` options. If the given values are
unacceptable, `undefined` will be returned.

