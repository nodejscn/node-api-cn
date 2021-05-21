<!-- YAML
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/33647
    description: Server.connections has been removed.
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.9.7
    pr-url: https://github.com/nodejs/node-v0.x-archive/pull/4595
    description: Runtime deprecation.
-->

Type: End-of-Life

The `Server.connections` property was deprecated in Node.js v0.9.7 and has
been removed. Please use the [`Server.getConnections()`][] method instead.

