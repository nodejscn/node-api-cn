<!-- YAML
added: v10.5.0
-->

* `exitCode` {integer}

The `'exit'` event is emitted once the worker has stopped. If the worker
exited by calling [`process.exit()`][], the `exitCode` parameter is the
passed exit code. If the worker was terminated, the `exitCode` parameter is
`1`.

This is the final event emitted by any `Worker` instance.

