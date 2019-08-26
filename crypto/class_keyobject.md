<!-- YAML
added: v11.6.0
changes:
  - version: v11.13.0
    pr-url: https://github.com/nodejs/node/pull/26438
    description: This class is now exported.
-->

Node.js uses a `KeyObject` class to represent a symmetric or asymmetric key,
and each kind of key exposes different functions. The
[`crypto.createSecretKey()`][], [`crypto.createPublicKey()`][] and
[`crypto.createPrivateKey()`][] methods are used to create `KeyObject`
instances. `KeyObject` objects are not to be created directly using the `new`
keyword.

Most applications should consider using the new `KeyObject` API instead of
passing keys as strings or `Buffer`s due to improved security features.

