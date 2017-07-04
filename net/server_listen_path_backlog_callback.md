<!-- YAML
added: v0.1.90
-->

* `path` {String} Path the server should listen to. See
  [Identifying paths for IPC connections][].
* `backlog` {number} Common parameter of [`server.listen()`][] functions
* `callback` {Function} Common parameter of [`server.listen()`][] functions
* Returns: {net.Server}

Start a [IPC][] server listening for connections on the given `path`.

