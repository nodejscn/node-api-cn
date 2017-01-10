<!-- YAML
added: v0.11.12
-->

* `command` {String} The command to run
* `options` {Object}
  * `cwd` {String} Current working directory of the child process
  * `input` {String|Buffer} The value which will be passed as stdin to the
    spawned process
    - supplying this value will override `stdio[0]`
  * `stdio` {String | Array} Child's stdio configuration. (Default: `'pipe'`)
    - `stderr` by default will be output to the parent process' stderr unless
      `stdio` is specified
  * `env` {Object} Environment key-value pairs
  * `shell` {String} Shell to execute the command with
    (Default: `'/bin/sh'` on UNIX, `'cmd.exe'` on Windows, The shell should
     understand the `-c` switch on UNIX or `/s /c` on Windows. On Windows,
     command line parsing should be compatible with `cmd.exe`.)
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
* return: {Buffer|String} The stdout from the command

The `child_process.execSync()` method is generally identical to
[`child_process.exec()`][] with the exception that the method will not return until
the child process has fully closed. When a timeout has been encountered and
`killSignal` is sent, the method won't return until the process has completely
exited. *Note that if  the child process intercepts and handles the `SIGTERM`
signal and doesn't exit, the parent process will wait until the child
process has exited.*

If the process times out, or has a non-zero exit code, this method ***will***
throw.  The [`Error`][] object will contain the entire result from
[`child_process.spawnSync()`][]

