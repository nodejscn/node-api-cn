<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22089
    description: Runtime deprecation.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19343
    description: Documentation-only deprecation.
-->

Type: Runtime

Using [`crypto.createCipher()`][] and [`crypto.createDecipher()`][] should be
avoided as they use a weak key derivation function (MD5 with no salt) and static
initialization vectors. It is recommended to derive a key using
[`crypto.pbkdf2()`][] or [`crypto.scrypt()`][] and to use
[`crypto.createCipheriv()`][] and [`crypto.createDecipheriv()`][] to obtain the
[`Cipher`][] and [`Decipher`][] objects respectively.

<a id="DEP0107"></a>
