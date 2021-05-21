<!-- YAML
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/33286
    description: End-of-Life.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/16242
    description: Runtime deprecation.
-->

Type: End-of-Life

`REPLServer.prototype.memory()` is only necessary for the internal mechanics of
the `REPLServer` itself. Do not use this function.

