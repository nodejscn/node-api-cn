<!-- YAML
changes:
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.11.14
    description: Runtime deprecation.
  - version: v0.5.11
    description: Documentation-only deprecation.
-->

Type: Runtime

Within the [`child_process`][] module's `spawn()`, `fork()`, and `exec()`
methods, the `options.customFds` option is deprecated. The `options.stdio`
option should be used instead.

<a id="DEP0007"></a>
