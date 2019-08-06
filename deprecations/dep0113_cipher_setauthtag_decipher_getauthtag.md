<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26249
    description: End-of-Life.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22126
    description: Runtime deprecation.
-->

Type: End-of-Life

`Cipher.setAuthTag()` and `Decipher.getAuthTag()` are no longer available. They
were never documented and would throw when called.

<a id="DEP0114"></a>
