<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22011
    description: Runtime deprecation.
-->

Type: Runtime

The `dgram` module previously contained several APIs that were never meant to
accessed outside of Node.js core: `Socket.prototype._handle`,
`Socket.prototype._receiving`, `Socket.prototype._bindState`,
`Socket.prototype._queue`, `Socket.prototype._reuseAddr`,
`Socket.prototype._healthCheck()`, `Socket.prototype._stopReceiving()`, and
`dgram._createSocketHandle()`.

<a id="DEP0113"></a>
