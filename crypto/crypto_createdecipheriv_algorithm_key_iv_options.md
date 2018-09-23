<!-- YAML
added: v0.1.94
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/21447
    description: Ciphers in OCB mode are now supported.
  - version: v10.2.0
    pr-url: https://github.com/nodejs/node/pull/20039
    description: The `authTagLength` option can now be used to restrict accepted
                 GCM authentication tag lengths.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/18644
    description: The `iv` parameter may now be `null` for ciphers which do not
                 need an initialization vector.
-->
* `algorithm` {string}
* `key` {string | Buffer | TypedArray | DataView}
* `iv` {string | Buffer | TypedArray | DataView}
* `options` {Object} [`stream.transform` options][]
* Returns: {Decipher}

Creates and returns a `Decipher` object that uses the given `algorithm`, `key`
and initialization vector (`iv`).

The `options` argument controls stream behavior and is optional except when a
cipher in CCM or OCB mode is used (e.g. `'aes-128-ccm'`). In that case, the
`authTagLength` option is required and specifies the length of the
authentication tag in bytes, see [CCM mode][]. In GCM mode, the `authTagLength`
option is not required but can be used to restrict accepted authentication tags
to those with the specified length.

The `algorithm` is dependent on OpenSSL, examples are `'aes192'`, etc. On
recent OpenSSL releases, `openssl list -cipher-algorithms`
(`openssl list-cipher-algorithms` for older versions of OpenSSL) will
display the available cipher algorithms.

The `key` is the raw key used by the `algorithm` and `iv` is an
[initialization vector][]. Both arguments must be `'utf8'` encoded strings,
[Buffers][`Buffer`], `TypedArray`, or `DataView`s. If the cipher does not need
an initialization vector, `iv` may be `null`.

Initialization vectors should be unpredictable and unique; ideally, they will be
cryptographically random. They do not have to be secret: IVs are typically just
added to ciphertext messages unencrypted. It may sound contradictory that
something has to be unpredictable and unique, but does not have to be secret;
it is important to remember that an attacker must not be able to predict ahead
of time what a given IV will be.

