
Type: End-of-Life

The `repl` module's `REPL_MODE_MAGIC` constant, used for `replMode` option, has
been removed. Its behavior has been functionally identical to that of
`REPL_MODE_SLOPPY` since Node.js 6.0.0, when V8 5.0 was imported. Please use
`REPL_MODE_SLOPPY` instead.

The `NODE_REPL_MODE` environment variable is used to set the underlying
`replMode` of an interactive `node` session. Its value, `magic`, is also
removed. Please use `sloppy` instead.

<a id="DEP0066"></a>
