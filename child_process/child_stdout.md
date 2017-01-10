<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

A `Readable Stream` that represents the child process's `stdout`.

If the child was spawned with `stdio[1]` set to anything other than `'pipe'`,
then this will be `undefined`.

`child.stdout` is an alias for `child.stdio[1]`. Both properties will refer
to the same value.

