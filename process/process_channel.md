<!-- YAML
added: v7.1.0
-->

If the Node.js process was spawned with an IPC channel (see the
[Child Process][] documentation), the `process.channel`
property is a reference to the IPC channel. If no IPC channel exists, this
property is `undefined`.

