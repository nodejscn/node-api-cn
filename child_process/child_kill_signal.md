<!-- YAML
added: v0.1.90
-->

* `signal` {String}

The `child.kill()` methods sends a signal to the child process. If no argument
is given, the process will be sent the `'SIGTERM'` signal. See signal(7) for
a list of available signals.

```js
const spawn = require('child_process').spawn;
const grep = spawn('grep', ['ssh']);

grep.on('close', (code, signal) => {
  console.log(
    `child process terminated due to receipt of signal ${signal}`);
});

// Send SIGHUP to process
grep.kill('SIGHUP');
```

The [`ChildProcess`][] object may emit an [`'error'`][] event if the signal cannot be
delivered. Sending a signal to a child process that has already exited is not
an error but may have unforeseen consequences. Specifically, if the process
identifier (PID) has been reassigned to another process, the signal will be
delivered to that process instead which can have unexpected results.

Note that while the function is called `kill`, the signal delivered to the
child process may not actually terminate the process.

See kill(2) for reference.

Also note: on Linux, child processes of child processes will not be terminated
when attempting to kill their parent. This is likely to happen when running a
new process in a shell or with use of the `shell` option of `ChildProcess`, such
as in this example:

```js
'use strict';
const spawn = require('child_process').spawn;

let child = spawn('sh', ['-c',
  `node -e "setInterval(() => {
      console.log(process.pid, 'is alive')
    }, 500);"`
  ], {
    stdio: ['inherit', 'inherit', 'inherit']
  });

setTimeout(() => {
  child.kill(); // does not terminate the node process in the shell
}, 2000);
```

