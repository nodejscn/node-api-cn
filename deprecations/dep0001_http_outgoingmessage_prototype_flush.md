<!-- YAML
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31164
    description: End-of-Life.
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v1.6.0
    pr-url: https://github.com/nodejs/node/pull/1156
    description: Runtime deprecation.
-->

Type: End-of-Life

`OutgoingMessage.prototype.flush()` has been removed. Use
`OutgoingMessage.prototype.flushHeaders()` instead.

