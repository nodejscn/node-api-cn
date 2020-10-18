<!-- YAML
added: v11.6.0
changes:
  - version: v13.9.0
    pr-url: https://github.com/nodejs/node/pull/31178
    description: Added support for `'dh'`.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26960
    description: Added support for `'rsa-pss'`.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26786
    description: This property now returns `undefined` for KeyObject
                 instances of unrecognized type instead of aborting.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26774
    description: Added support for `'x25519'` and `'x448'`.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26319
    description: Added support for `'ed25519'` and `'ed448'`.
-->

* {string}

For asymmetric keys, this property represents the type of the key. Supported key
types are:

* `'rsa'` (OID 1.2.840.113549.1.1.1)
* `'rsa-pss'` (OID 1.2.840.113549.1.1.10)
* `'dsa'` (OID 1.2.840.10040.4.1)
* `'ec'` (OID 1.2.840.10045.2.1)
* `'x25519'` (OID 1.3.101.110)
* `'x448'` (OID 1.3.101.111)
* `'ed25519'` (OID 1.3.101.112)
* `'ed448'` (OID 1.3.101.113)
* `'dh'` (OID 1.2.840.113549.1.3.1)

This property is `undefined` for unrecognized `KeyObject` types and symmetric
keys.

