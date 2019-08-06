<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/23597
    description: Documentation-only deprecation.
-->

Type: Documentation-only (supports [`--pending-deprecation`][])

`process.binding('uv').errname()` is deprecated. Please use
[`util.getSystemErrorName()`][] instead.

<a id="DEP0120"></a>
