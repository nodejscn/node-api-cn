<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19353
    description: Runtime deprecation.
-->

Type: Runtime

`decipher.finaltol()` has never been documented and is currently an alias for
[`decipher.final()`][]. In the future, this API will likely be removed, and it
is recommended to use [`decipher.final()`][] instead.

<a id="DEP0106"></a>
