
The `process.stderr` and `process.stdout` streams are blocking when outputting
to TTYs (terminals) on OS X as a workaround for the operating system's small,
1kb buffer size. This is to prevent interleaving between `stdout` and `stderr`.

To check if Node.js is being run in a [TTY][] context, check the `isTTY`
property on `process.stderr`, `process.stdout`, or `process.stdin`.

For instance:
```console
$ node -p "Boolean(process.stdin.isTTY)"
true
$ echo "foo" | node -p "Boolean(process.stdin.isTTY)"
false

$ node -p "Boolean(process.stdout.isTTY)"
true
$ node -p "Boolean(process.stdout.isTTY)" | cat
false
```

See the [TTY][] documentation for more information.

