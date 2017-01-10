<!-- YAML
added: v0.7.0
-->

* {ChildProcess}

All workers are created using [`child_process.fork()`][], the returned object
from this function is stored as `.process`. In a worker, the global `process`
is stored.

See: [Child Process module][]

Note that workers will call `process.exit(0)` if the `'disconnect'` event occurs
on `process` and `.exitedAfterDisconnect` is not `true`. This protects against
accidental disconnection.

