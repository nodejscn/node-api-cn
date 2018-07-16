
<!--introduced_in=v10.5.0-->

> Stability: 1 - Experimental

The `worker` module provides a way to create multiple environments running
on independent threads, and to create message channels between them. It
can be accessed using the `--experimental-worker` flag and:

```js
const worker = require('worker_threads');
```

Workers are useful for performing CPU-intensive JavaScript operations; do not
use them for I/O, since Node.js’s built-in mechanisms for performing operations
asynchronously already treat it more efficiently than Worker threads can.

Workers, unlike child processes or when using the `cluster` module, can also
share memory efficiently by transferring `ArrayBuffer` instances or sharing
`SharedArrayBuffer` instances between them.

