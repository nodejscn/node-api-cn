<!-- YAML
added: v0.2.0
deprecated: v0.9.7
-->

> Stability: 0 - Deprecated: Use [`server.getConnections()`][] instead.

The number of concurrent connections on the server.

This becomes `null` when sending a socket to a child with
[`child_process.fork()`][]. To poll forks and get current number of active
connections use asynchronous [`server.getConnections()`][] instead.

