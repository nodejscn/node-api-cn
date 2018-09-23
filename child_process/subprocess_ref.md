<!-- YAML
added: v0.7.10
-->

Calling `subprocess.ref()` after making a call to `subprocess.unref()` will
restore the removed reference count for the child process, forcing the parent
to wait for the child to exit before exiting itself.

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
subprocess.ref();
```

