<!-- YAML
added: v0.11.12
-->

* `command` {String} The command to run
* `args` {Array} List of string arguments
* `options` {Object}
  * `cwd` {String} Current working directory of the child process
  * `input` {String|Buffer} The value which will be passed as stdin to the
    spawned process
    - supplying this value will override `stdio[0]`
  * `stdio` {String | Array} Child's stdio configuration.
  * `env` {Object} Environment key-value pairs
  * `uid` {Number} Sets the user identity of the process. (See setuid(2).)
  * `gid` {Number} Sets the group identity of the process. (See setgid(2).)
  * `timeout` {Number} In milliseconds the maximum amount of time the process
    is allowed to run. (Default: `undefined`)
  * `killSignal` {String} The signal value to be used when the spawned process
    will be killed. (Default: `'SIGTERM'`)
  * [`maxBuffer`][] {Number} largest amount of data (in bytes) allowed on
    stdout or stderr - if exceeded child process is killed
  * `encoding` {String} The encoding used for all stdio inputs and outputs.
    (Default: `'buffer'`)
  * `shell` {Boolean|String} If `true`, runs `command` inside of a shell. Uses
    `'/bin/sh'` on UNIX, and `'cmd.exe'` on Windows. A different shell can be
    specified as a string. The shell should understand the `-c` switch on UNIX,
    or `/s /c` on Windows. Defaults to `false` (no shell).
* return: {Object}
  * `pid` {Number} Pid of the child process
  * `output` {Array} Array of results from stdio output
  * `stdout` {Buffer|String} The contents of `output[1]`
  * `stderr` {Buffer|String} The contents of `output[2]`
  * `status` {Number} The exit code of the child process
  * `signal` {String} The signal used to kill the child process
  * `error` {Error} The error object if the child process failed or timed out

The `child_process.spawnSync()` method is generally identical to
[`child_process.spawn()`][] with the exception that the function will not return
until the child process has fully closed. When a timeout has been encountered
and `killSignal` is sent, the method won't return until the process has
completely exited. Note that if the process intercepts and handles the
`SIGTERM` signal and doesn't exit, the parent process will wait until the child
process has exited.

