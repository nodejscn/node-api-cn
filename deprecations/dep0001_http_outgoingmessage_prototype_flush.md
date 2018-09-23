<!-- YAML
changes:
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v1.6.0
    pr-url: https://github.com/nodejs/node/pull/1156
    description: Runtime deprecation.
-->

Type: Runtime

The `OutgoingMessage.prototype.flush()` method is deprecated. Use
`OutgoingMessage.prototype.flushHeaders()` instead.

<a id="DEP0002"></a>
