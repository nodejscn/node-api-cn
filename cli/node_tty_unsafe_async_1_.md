<!-- YAML
added: 6.4.0
-->

When set to `1`, writes to `stdout` and `stderr` will be non-blocking and
asynchronous when outputting to a TTY on platforms which support async stdio.
Setting this will void any guarantee that stdio will not be interleaved or
dropped at program exit. **Use of this mode is not recommended.**


[Buffer]: buffer.html#buffer_buffer
[debugger]: debugger.html
[REPL]: repl.html
[SlowBuffer]: buffer.html#buffer_class_slowbuffer
