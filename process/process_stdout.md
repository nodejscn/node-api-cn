
* {Stream}

The `process.stdout` property returns a [Writable][] stream equivalent to or
associated with `stdout` (fd `1`).

For example:

```js
console.log = (msg) => {
  process.stdout.write(`${msg}\n`);
};
```

Note: `process.stderr` and `process.stdout` differ from other Node.js streams
in several ways:
1. They cannot be closed ([`end()`][] will throw).
2. They never emit the [`'finish'`][] event.
3. Writes _can_ block when output is redirected to a file.
  - Note that disks are fast and operating systems normally employ write-back
    caching so this is very uncommon.
4. Writes on UNIX **will** block by default if output is going to a TTY
   (a terminal).
5. Windows functionality differs. Writes block except when output is going to a
   TTY.

To check if Node.js is being run in a TTY context, read the `isTTY` property
on `process.stderr`, `process.stdout`, or `process.stdin`:

