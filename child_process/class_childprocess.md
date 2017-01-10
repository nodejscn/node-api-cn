<!-- YAML
added: v2.2.0
-->

Instances of the `ChildProcess` class are [`EventEmitters`][`EventEmitter`] that represent
spawned child processes.

Instances of `ChildProcess` are not intended to be created directly. Rather,
use the [`child_process.spawn()`][], [`child_process.exec()`][],
[`child_process.execFile()`][], or [`child_process.fork()`][] methods to create
instances of `ChildProcess`.

