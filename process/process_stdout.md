
* {Stream}

The `process.stdout` property returns a [Writable][] stream connected to
`stdout` (fd `2`).

For example, to copy process.stdin to process.stdout:

```js
process.stdin.pipe(process.stdout);
```

Note: `process.stdout` differs from other Node.js streams in important ways,
see [note on process I/O][] for more information.

