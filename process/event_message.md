<!-- YAML
added: v0.5.10
-->

If the Node.js process is spawned with an IPC channel (see the [Child Process][]
and [Cluster][] documentation), the `'message'` event is emitted whenever a
message sent by a parent process using [`childprocess.send()`][] is received by
the child process.

The listener callback is invoked with the following arguments:
* `message` {Object} a parsed JSON object or primitive value
* `sendHandle` {Handle object} a [`net.Socket`][] or [`net.Server`][] object, or
  undefined.


