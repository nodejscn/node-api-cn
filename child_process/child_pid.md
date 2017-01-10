<!-- YAML
added: v0.1.90
-->

* {Number} Integer

Returns the process identifier (PID) of the child process.

Example:

```js
const spawn = require('child_process').spawn;
const grep = spawn('grep', ['ssh']);

console.log(`Spawned child pid: ${grep.pid}`);
grep.stdin.end();
```

