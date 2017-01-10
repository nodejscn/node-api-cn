<!-- YAML
added: v0.11.12
-->

* `file` {String} The name or path of the executable file to run
* `args` {Array} List of string arguments
* `options` {Object}
  * `cwd` {String} Current working directory of the child process
  * `input` {String|Buffer} The value which will be passed as stdin to the
    spawned process
    - supplying this value will override `stdio[0]`
  * `stdio` {String | Array} Child's stdio configuration. (Default: `'pipe'`)
    - `stderr` by default will be output to the parent process' stderr unless
      `stdio` is specified
  * `env` {Object} Environment key-value pairs
  * `uid` {Number} Sets the user identity of the process. (See setuid(2).)
  * `gid` {Number} Sets the group identity of the process. (See setgid(2).)
  * `timeout` {Number} In milliseconds the maximum amount of time the process
    is allowed to run. (Default: `undefined`)
  * `killSignal` {String} The signal value to be used when the spawned process
    will be killed. (Default: `'SIGTERM'`)
  * [`maxBuffer`][] {Number} largest amount of data (in bytes) allowed on
    stdout or stderr - if exceeded child process is killed
  * `encoding` {String} The encoding used for all stdio inputs and outputs. (Default: `'buffer'`)
* return: {Buffer|String} The stdout from the command

The `child_process.execFileSync()` method is generally identical to
[`child_process.execFile()`][] with the exception that the method will not return
until the child process has fully closed. When a timeout has been encountered
and `killSignal` is sent, the method won't return until the process has
completely exited. *Note that if the child process intercepts and handles
the `SIGTERM` signal and does not exit, the parent process will still wait
until the child process has exited.*

If the process times out, or has a non-zero exit code, this method ***will***
throw.  The [`Error`][] object will contain the entire result from
[`child_process.spawnSync()`][]

