<!-- YAML
added: v0.1.90
-->

* {stream.Writable}

A `Writable Stream` that represents the child process's `stdin`.

*Note that if a child process waits to read all of its input, the child will not
continue until this stream has been closed via `end()`.*

If the child was spawned with `stdio[0]` set to anything other than `'pipe'`,
then this will be `undefined`.

`child.stdin` is an alias for `child.stdio[0]`. Both properties will refer to
the same value.

