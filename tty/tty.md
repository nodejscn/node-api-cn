
> Stability: 2 - Stable

The `tty` module provides the `tty.ReadStream` and `tty.WriteStream` classes.
In most cases, it will not be necessary or possible to use this module directly.
However, it can be accessed using:

```js
const tty = require('tty');
```

When Node.js detects that it is being run inside a text terminal ("TTY")
context, the `process.stdin` will, by default, be initialized as an instance of
`tty.ReadStream` and both `process.stdout` and `process.stderr` will, by
default be instances of `tty.WriteStream`. The preferred method of determining
whether Node.js is being run within a TTY context is to check that the value of
the `process.stdout.isTTY` property is `true`:

```sh
$ node -p -e "Boolean(process.stdout.isTTY)"
true
$ node -p -e "Boolean(process.stdout.isTTY)" | cat
false
```

In most cases, there should be little to no reason for an application to
create instances of the `tty.ReadStream` and `tty.WriteStream` classes.

