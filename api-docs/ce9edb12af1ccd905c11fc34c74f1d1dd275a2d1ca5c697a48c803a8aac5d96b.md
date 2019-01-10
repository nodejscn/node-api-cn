<!-- YAML
changes:
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v1.8.1
    pr-url: https://github.com/nodejs/node/pull/1363
    description: Runtime deprecation.
-->

Type: Runtime

In certain cases, `require('.')` may resolve outside the package directory.
This behavior is deprecated and will be removed in a future major Node.js
release.

<a id="DEP0020"></a>
