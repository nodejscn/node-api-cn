<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

A `Readable Stream` that represents the child process's `stderr`.

If the child was spawned with `stdio[2]` set to anything other than `'pipe'`,
then this will be `undefined`.

`child.stderr` is an alias for `child.stdio[2]`. Both properties will refer to
the same value.

