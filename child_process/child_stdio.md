<!-- YAML
added: v0.7.10
-->

* {Array}

A sparse array of pipes to the child process, corresponding with positions in
the [`stdio`][] option passed to [`child_process.spawn()`][] that have been set
to the value `'pipe'`. Note that `child.stdio[0]`, `child.stdio[1]`, and
`child.stdio[2]` are also available as `child.stdin`, `child.stdout`, and
`child.stderr`, respectively.

In the following example, only the child's fd `1` (stdout) is configured as a
pipe, so only the parent's `child.stdio[1]` is a stream, all other values in
the array are `null`.

```js
const assert = require('assert');
const fs = require('fs');
const child_process = require('child_process');

const child = child_process.spawn('ls', {
    stdio: [
      0, // Use parents stdin for child
      'pipe', // Pipe child's stdout to parent
      fs.openSync('err.out', 'w') // Direct child's stderr to a file
    ]
});

assert.equal(child.stdio[0], null);
assert.equal(child.stdio[0], child.stdin);

assert(child.stdout);
assert.equal(child.stdio[1], child.stdout);

assert.equal(child.stdio[2], null);
assert.equal(child.stdio[2], child.stderr);
```

