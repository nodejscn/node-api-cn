
<!--type=event-->
<!--name=SIGINT, SIGHUP, etc.-->

Signal events will be emitted when the Node.js process receives a signal. Please
refer to signal(7) for a listing of standard POSIX signal names such as
`SIGINT`, `SIGHUP`, etc.

The name of each event will be the uppercase common name for the signal (e.g.
`'SIGINT'` for `SIGINT` signals).

For example:

```js
// Begin reading from stdin so the process does not exit.
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('Received SIGINT.  Press Control-D to exit.');
});
```

*Note*: An easy way to send the `SIGINT` signal is with `<Ctrl>-C` in most
terminal programs.

It is important to take note of the following:

* `SIGUSR1` is reserved by Node.js to start the debugger.  It's possible to
  install a listener but doing so will _not_ stop the debugger from starting.
* `SIGTERM` and `SIGINT` have default handlers on non-Windows platforms that
  resets the terminal mode before exiting with code `128 + signal number`. If
  one of these signals has a listener installed, its default behavior will be
  removed (Node.js will no longer exit).
* `SIGPIPE` is ignored by default. It can have a listener installed.
* `SIGHUP` is generated on Windows when the console window is closed, and on
  other platforms under various similar conditions, see signal(7). It can have a
  listener installed, however Node.js will be unconditionally terminated by
  Windows about 10 seconds later. On non-Windows platforms, the default
  behavior of `SIGHUP` is to terminate Node.js, but once a listener has been
  installed its default behavior will be removed.
* `SIGTERM` is not supported on Windows, it can be listened on.
* `SIGINT` from the terminal is supported on all platforms, and can usually be
  generated with `CTRL+C` (though this may be configurable). It is not generated
  when terminal raw mode is enabled.
* `SIGBREAK` is delivered on Windows when `<Ctrl>+<Break>` is pressed, on
  non-Windows platforms it can be listened on, but there is no way to send or
  generate it.
* `SIGWINCH` is delivered when the console has been resized. On Windows, this
  will only happen on write to the console when the cursor is being moved, or
  when a readable tty is used in raw mode.
* `SIGKILL` cannot have a listener installed, it will unconditionally terminate
  Node.js on all platforms.
* `SIGSTOP` cannot have a listener installed.
* `SIGBUS`, `SIGFPE`, `SIGSEGV` and `SIGILL`, when not raised artificially
   using kill(2), inherently leave the process in a state from which it is not
   safe to attempt to call JS listeners. Doing so might lead to the process
   hanging in an endless loop, since listeners attached using `process.on()` are
   called asynchronously and therefore unable to correct the underlying problem.

*Note*: Windows does not support sending signals, but Node.js offers some
emulation with [`process.kill()`][], and [`ChildProcess.kill()`][]. Sending
signal `0` can be used to test for the existence of a process. Sending `SIGINT`,
`SIGTERM`, and `SIGKILL` cause the unconditional termination of the target
process.

