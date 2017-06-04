<!-- YAML
added: v0.1.94
-->
- `algorithm` {string}
- `key` {string | Buffer | TypedArray | DataView}
- `iv` {string | Buffer | TypedArray | DataView}

Creates and returns a `Decipher` object that uses the given `algorithm`, `key`
and initialization vector (`iv`).

The `algorithm` is dependent on OpenSSL, examples are `'aes192'`, etc. On
recent OpenSSL releases, `openssl list-cipher-algorithms` will display the
available cipher algorithms.

The `key` is the raw key used by the `algorithm` and `iv` is an
[initialization vector][]. Both arguments must be `'utf8'` encoded strings or
[buffers][`Buffer`].

