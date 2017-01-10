<!-- YAML
added: v0.1.90
-->

* `code` {Number} the exit code if the child exited on its own.
* `signal` {String} the signal by which the child process was terminated.

The `'exit'` event is emitted after the child process ends. If the process
exited, `code` is the final exit code of the process, otherwise `null`. If the
process terminated due to receipt of a signal, `signal` is the string name of
the signal, otherwise `null`. One of the two will always be non-null.

Note that when the `'exit'` event is triggered, child process stdio streams
might still be open.

Also, note that Node.js establishes signal handlers for `SIGINT` and
`SIGTERM` and Node.js processes will not terminate immediately due to receipt
of those signals. Rather, Node.js will perform a sequence of cleanup actions
and then will re-raise the handled signal.

See waitpid(2).

