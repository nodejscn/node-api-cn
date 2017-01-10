<!-- YAML
added: v0.1.90
-->

* `command` {String} The command to run, with space-separated arguments
* `options` {Object}
  * `cwd` {String} Current working directory of the child process
  * `env` {Object} Environment key-value pairs
  * `encoding` {String} (Default: `'utf8'`)
  * `shell` {String} Shell to execute the command with
    (Default: `'/bin/sh'` on UNIX, `'cmd.exe'` on Windows, The shell should
     understand the `-c` switch on UNIX or `/s /c` on Windows. On Windows,
     command line parsing should be compatible with `cmd.exe`.)
  * `timeout` {Number} (Default: `0`)
  * [`maxBuffer`][] {Number} largest amount of data (in bytes) allowed on
    stdout or stderr - if exceeded child process is killed (Default: `200*1024`)
  * `killSignal` {String} (Default: `'SIGTERM'`)
  * `uid` {Number} Sets the user identity of the process. (See setuid(2).)
  * `gid` {Number} Sets the group identity of the process. (See setgid(2).)
* `callback` {Function} called with the output when process terminates
  * `error` {Error}
  * `stdout` {String|Buffer}
  * `stderr` {String|Buffer}
* Returns: {ChildProcess}

Spawns a shell then executes the `command` within that shell, buffering any
generated output.

```js
const exec = require('child_process').exec;
exec('cat *.js bad_file | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});
```

If a `callback` function is provided, it is called with the arguments
`(error, stdout, stderr)`. On success, `error` will be `null`.  On error,
`error` will be an instance of [`Error`][]. The `error.code` property will be
the exit code of the child process while `error.signal` will be set to the
signal that terminated the process. Any exit code other than `0` is considered
to be an error.

The `stdout` and `stderr` arguments passed to the callback will contain the
stdout and stderr output of the child process. By default, Node.js will decode
the output as UTF-8 and pass strings to the callback. The `encoding` option
can be used to specify the character encoding used to decode the stdout and
stderr output. If `encoding` is `'buffer'`, or an unrecognized character
encoding, `Buffer` objects will be passed to the callback instead.

The `options` argument may be passed as the second argument to customize how
the process is spawned. The default options are:

```js
{
  encoding: 'utf8',
  timeout: 0,
  maxBuffer: 200*1024,
  killSignal: 'SIGTERM',
  cwd: null,
  env: null
}
```

If `timeout` is greater than `0`, the parent will send the the signal
identified by the `killSignal` property (the default is `'SIGTERM'`) if the
child runs longer than `timeout` milliseconds.

*Note: Unlike the exec(3) POSIX system call, `child_process.exec()` does not
replace the existing process and uses a shell to execute the command.*

