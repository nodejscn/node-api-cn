<!-- YAML
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/16242
    description: Runtime deprecation.
-->

Type: Runtime

`REPLServer.prototype.memory()` is only necessary for the internal mechanics of
the `REPLServer` itself. Do not use this function.

<a id="DEP0083"></a>
