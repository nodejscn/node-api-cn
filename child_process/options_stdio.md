<!-- YAML
added: v0.7.10
-->

The `options.stdio` option is used to configure the pipes that are established
between the parent and child process. By default, the child's stdin, stdout,
and stderr are redirected to corresponding [`child.stdin`][], [`child.stdout`][], and
[`child.stderr`][] streams on the [`ChildProcess`][] object. This is equivalent to
setting the `options.stdio` equal to `['pipe', 'pipe', 'pipe']`.

For convenience, `options.stdio` may be one of the following strings:

* `'pipe'` - equivalent to `['pipe', 'pipe', 'pipe']` (the default)
* `'ignore'` - equivalent to `['ignore', 'ignore', 'ignore']`
* `'inherit'` - equivalent to `[process.stdin, process.stdout, process.stderr]`
   or `[0,1,2]`

Otherwise, the value of `options.stdio` is an array where each index corresponds
to an fd in the child. The fds 0, 1, and 2 correspond to stdin, stdout,
and stderr, respectively. Additional fds can be specified to create additional
pipes between the parent and child. The value is one of the following:

1. `'pipe'` - Create a pipe between the child process and the parent process.
   The parent end of the pipe is exposed to the parent as a property on the
   `child_process` object as [`child.stdio[fd]`][`stdio`]. Pipes created for
   fds 0 - 2 are also available as [`child.stdin`][], [`child.stdout`][]
   and [`child.stderr`][], respectively.
2. `'ipc'` - Create an IPC channel for passing messages/file descriptors
   between parent and child. A [`ChildProcess`][] may have at most *one* IPC stdio
   file descriptor. Setting this option enables the [`child.send()`][] method.
   If the child writes JSON messages to this file descriptor, the
   [`child.on('message')`][`'message'`] event handler will be triggered in the parent.
   If the child is a Node.js process, the presence of an IPC channel will enable
   [`process.send()`][], [`process.disconnect()`][], [`process.on('disconnect')`][], and
   [`process.on('message')`] within the child.
3. `'ignore'` - Instructs Node.js to ignore the fd in the child. While Node.js
   will always open fds 0 - 2 for the processes it spawns, setting the fd to
   `'ignore'` will cause Node.js to open `/dev/null` and attach it to the
   child's fd.
4. {Stream} object - Share a readable or writable stream that refers to a tty,
   file, socket, or a pipe with the child process. The stream's underlying
   file descriptor is duplicated in the child process to the fd that
   corresponds to the index in the `stdio` array. Note that the stream must
   have an underlying descriptor (file streams do not until the `'open'`
   event has occurred).
5. Positive integer - The integer value is interpreted as a file descriptor
   that is is currently open in the parent process. It is shared with the child
   process, similar to how {Stream} objects can be shared.
6. `null`, `undefined` - Use default value. For stdio fds 0, 1 and 2 (in other
   words, stdin, stdout, and stderr) a pipe is created. For fd 3 and up, the
   default is `'ignore'`.

Example:

```js
const spawn = require('child_process').spawn;

// Child will use parent's stdios
spawn('prg', [], { stdio: 'inherit' });

// Spawn child sharing only stderr
spawn('prg', [], { stdio: ['pipe', 'pipe', process.stderr] });

// Open an extra fd=4, to interact with programs presenting a
// startd-style interface.
spawn('prg', [], { stdio: ['pipe', null, null, null, 'pipe'] });
```

*It is worth noting that when an IPC channel is established between the
parent and child processes, and the child is a Node.js process, the child
is launched with the IPC channel unreferenced (using `unref()`) until the
child registers an event handler for the [`process.on('disconnect')`][] event.
This allows the child to exit normally without the process being held open
by the open IPC channel.*

See also: [`child_process.exec()`][] and [`child_process.fork()`][]

