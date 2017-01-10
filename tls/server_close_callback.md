<!-- YAML
added: v0.3.2
-->

* `callback` {Function} An optional listener callback that will be registered to
  listen for the server instance's `'close'` event.

The `server.close()` method stops the server from accepting new connections.

This function operates asynchronously. The `'close'` event will be emitted
when the server has no more open connections.

