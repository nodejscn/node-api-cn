<!-- YAML
added: v0.7.10
-->

On Windows, setting `options.detached` to `true` makes it possible for the
child process to continue running after the parent exits. The child will have
its own console window. *Once enabled for a child process, it cannot be
disabled*.

On non-Windows platforms, if `options.detached` is set to `true`, the child
process will be made the leader of a new process group and session. Note that
child processes may continue running after the parent exits regardless of
whether they are detached or not.  See setsid(2) for more information.

By default, the parent will wait for the detached child to exit. To prevent
the parent from waiting for a given `child`, use the `child.unref()` method.
Doing so will cause the parent's event loop to not include the child in its
reference count, allowing the parent to exit independently of the child, unless
there is an established IPC channel between the child and parent.

When using the `detached` option to start a long-running process, the process
will not stay running in the background after the parent exits unless it is
provided with a `stdio` configuration that is not connected to the parent.
If the parent's `stdio` is inherited, the child will remain attached to the
controlling terminal.

Example of a long-running process, by detaching and also ignoring its parent
`stdio` file descriptors, in order to ignore the parent's termination:

```js
const spawn = require('child_process').spawn;

const child = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

child.unref();
```

Alternatively one can redirect the child process' output into files:

```js
const fs = require('fs');
const spawn = require('child_process').spawn;
const out = fs.openSync('./out.log', 'a');
const err = fs.openSync('./out.log', 'a');

const child = spawn('prg', [], {
 detached: true,
 stdio: [ 'ignore', out, err ]
});

child.unref();
```

