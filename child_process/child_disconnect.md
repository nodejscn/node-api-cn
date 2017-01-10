<!-- YAML
added: v0.7.2
-->

Closes the IPC channel between parent and child, allowing the child to exit
gracefully once there are no other connections keeping it alive. After calling
this method the `child.connected` and `process.connected` properties in both
the parent and child (respectively) will be set to `false`, and it will be no
longer possible to pass messages between the processes.

The `'disconnect'` event will be emitted when there are no messages in the
process of being received. This will most often be triggered immediately after
calling `child.disconnect()`.

Note that when the child process is a Node.js instance (e.g. spawned using
[`child_process.fork()`]), the `process.disconnect()` method can be invoked
within the child process to close the IPC channel as well.

