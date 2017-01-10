<!-- YAML
added: v0.7.7
-->

If the Node.js process is spawned with an IPC channel (see the [Child Process][]
and [Cluster][] documentation), the `'disconnect'` event will be emitted when
the IPC channel is closed.

