<!-- YAML
added: v10.5.0
-->

* {stream.Readable}

This is a readable stream which contains data written to [`process.stdout`][]
inside the worker thread. If `stdout: true` was not passed to the
[`Worker`][] constructor, then data is piped to the parent thread's
[`process.stdout`][] stream.

