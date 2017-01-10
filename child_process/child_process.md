
> Stability: 2 - Stable

The `child_process` module provides the ability to spawn child processes in
a manner that is similar, but not identical, to popen(3). This capability
is primarily provided by the [`child_process.spawn()`][] function:

```js
const spawn = require('child_process').spawn;
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.log(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});
```

By default, pipes for `stdin`, `stdout` and `stderr` are established between
the parent Node.js process and the spawned child. It is possible to stream data
through these pipes in a non-blocking way. *Note, however, that some programs
use line-buffered I/O internally. While that does not affect Node.js, it can
mean that data sent to the child process may not be immediately consumed.*

The [`child_process.spawn()`][] method spawns the child process asynchronously,
without blocking the Node.js event loop. The [`child_process.spawnSync()`][]
function provides equivalent functionality in a synchronous manner that blocks
the event loop until the spawned process either exits or is terminated.

For convenience, the `child_process` module provides a handful of synchronous
and asynchronous alternatives to [`child_process.spawn()`][] and
[`child_process.spawnSync()`][].  *Note that each of these alternatives are
implemented on top of [`child_process.spawn()`][] or [`child_process.spawnSync()`][].*

  * [`child_process.exec()`][]: spawns a shell and runs a command within that shell,
    passing the `stdout` and `stderr` to a callback function when complete.
  * [`child_process.execFile()`][]: similar to [`child_process.exec()`][] except that
    it spawns the command directly without first spawning a shell.
  * [`child_process.fork()`][]: spawns a new Node.js process and invokes a
    specified module with an IPC communication channel established that allows
    sending messages between parent and child.
  * [`child_process.execSync()`][]: a synchronous version of
    [`child_process.exec()`][] that *will* block the Node.js event loop.
  * [`child_process.execFileSync()`][]: a synchronous version of
    [`child_process.execFile()`][] that *will* block the Node.js event loop.

For certain use cases, such as automating shell scripts, the
[synchronous counterparts][] may be more convenient. In many cases, however,
the synchronous methods can have significant impact on performance due to
stalling the event loop while spawned processes complete.

