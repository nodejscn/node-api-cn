<!-- YAML
changes:
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v1.0.0
    pr-url: https://github.com/iojs/io.js/pull/166
    description: Documentation-only deprecation.
-->

Type: Documentation-only

The [`fs.exists(path, callback)`][] API is deprecated. Please use
[`fs.stat()`][] or [`fs.access()`][] instead.

<a id="DEP0035"></a>
