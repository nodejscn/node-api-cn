<!-- YAML
added: v5.10.0
-->

Node.js can be started using the `--zero-fill-buffers` command line option to
force all newly allocated `Buffer` instances created using either
`new Buffer(size)`, [`Buffer.allocUnsafe()`], [`Buffer.allocUnsafeSlow()`] or
`new SlowBuffer(size)` to be *automatically zero-filled* upon creation. Use of
this flag *changes the default behavior* of these methods and *can have a significant
impact* on performance. Use of the `--zero-fill-buffers` option is recommended
only when necessary to enforce that newly allocated `Buffer` instances cannot
contain potentially sensitive data.

Example:

```txt
$ node --zero-fill-buffers
> Buffer.allocUnsafe(5);
<Buffer 00 00 00 00 00>
```

