
Node.js will normally exit with a `0` status code when no more async
operations are pending.  The following status codes are used in other
cases:

* `1` **Uncaught Fatal Exception** - There was an uncaught exception,
  and it was not handled by a domain or an [`'uncaughtException'`][] event
  handler.
* `2` - Unused (reserved by Bash for builtin misuse)
* `3` **Internal JavaScript Parse Error** - The JavaScript source code
  internal in Node.js's bootstrapping process caused a parse error.  This
  is extremely rare, and generally can only happen during development
  of Node.js itself.
* `4` **Internal JavaScript Evaluation Failure** - The JavaScript
  source code internal in Node.js's bootstrapping process failed to
  return a function value when evaluated.  This is extremely rare, and
  generally can only happen during development of Node.js itself.
* `5` **Fatal Error** - There was a fatal unrecoverable error in V8.
  Typically a message will be printed to stderr with the prefix `FATAL
  ERROR`.
* `6` **Non-function Internal Exception Handler** - There was an
  uncaught exception, but the internal fatal exception handler
  function was somehow set to a non-function, and could not be called.
* `7` **Internal Exception Handler Run-Time Failure** - There was an
  uncaught exception, and the internal fatal exception handler
  function itself threw an error while attempting to handle it.  This
  can happen, for example, if a [`'uncaughtException'`][] or
  `domain.on('error')` handler throws an error.
* `8` - Unused.  In previous versions of Node.js, exit code 8 sometimes
  indicated an uncaught exception.
* `9` - **Invalid Argument** - Either an unknown option was specified,
  or an option requiring a value was provided without a value.
* `10` **Internal JavaScript Run-Time Failure** - The JavaScript
  source code internal in Node.js's bootstrapping process threw an error
  when the bootstrapping function was called.  This is extremely rare,
  and generally can only happen during development of Node.js itself.
* `12` **Invalid Debug Argument** - The `--debug`, `--inspect` and/or
  `--debug-brk` options were set, but the port number chosen was invalid
  or unavailable.
* `>128` **Signal Exits** - If Node.js receives a fatal signal such as
  `SIGKILL` or `SIGHUP`, then its exit code will be `128` plus the
  value of the signal code.  This is a standard Unix practice, since
  exit codes are defined to be 7-bit integers, and signal exits set
  the high-order bit, and then contain the value of the signal code.


[`'finish'`]: stream.html#stream_event_finish
[`'message'`]: child_process.html#child_process_event_message
[`'rejectionHandled'`]: #process_event_rejectionhandled
[`'uncaughtException'`]: #process_event_uncaughtexception
[`ChildProcess.disconnect()`]: child_process.html#child_process_child_disconnect
[`ChildProcess.kill()`]: child_process.html#child_process_child_kill_signal
[`ChildProcess.send()`]: child_process.html#child_process_child_send_message_sendhandle_options_callback
[`ChildProcess`]: child_process.html#child_process_class_childprocess
[`end()`]: stream.html#stream_writable_end_chunk_encoding_callback
[`Error`]: errors.html#errors_class_error
[`EventEmitter`]: events.html#events_class_eventemitter
[`JSON.stringify()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[`net.Server`]: net.html#net_class_net_server
[`net.Socket`]: net.html#net_class_net_socket
[`process.argv`]: #process_process_argv
[`process.exit()`]: #process_process_exit_code
[`process.kill()`]: #process_process_kill_pid_signal
[`process.execPath`]: #process_process_execpath
[`promise.catch()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch
[`require.main`]: modules.html#modules_accessing_the_main_module
[`setTimeout(fn, 0)`]: timers.html#timers_settimeout_callback_delay_args
[process_emit_warning]: #process_process_emitwarning_warning_name_ctor
[process_warning]: #process_event_warning
[Signal Events]: #process_signal_events
[Stream compatibility]: stream.html#stream_compatibility_with_older_node_js_versions
[TTY]: tty.html#tty_tty
[Writable]: stream.html
[Readable]: stream.html
[Child Process]: child_process.html
[Cluster]: cluster.html
[`process.exitCode`]: #processexitcode-1
[LTS]: https://github.com/nodejs/LTS/
