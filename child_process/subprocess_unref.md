<!-- YAML
added: v0.7.10
-->

By default, the parent will wait for the detached child to exit. To prevent the
parent from waiting for a given `subprocess` to exit, use the
`subprocess.unref()` method. Doing so will cause the parent's event loop to not
include the child in its reference count, allowing the parent to exit
independently of the child, unless there is an established IPC channel between
the child and the parent.

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
```

