<!-- YAML
added: v0.11.14
-->

This function returns `true` if the worker is connected to its master via its
IPC channel, `false` otherwise. A worker is connected to its master after it
has been created. It is disconnected after the `'disconnect'` event is emitted.

