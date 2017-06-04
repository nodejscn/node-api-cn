
Type: Documentation-only

The `repl` module's `REPL_MODE_MAGIC` constant, used for `replMode` option, has
been deprecated. Its behavior has been functionally identical to that of
`REPL_MODE_SLOPPY` since Node.js v6.0.0, when V8 5.0 was imported. Please use
`REPL_MODE_SLOPPY` instead.

The `NODE_REPL_MODE` environment variable is used to set the underlying
`replMode` of an interactive `node` session. Its default value, `magic`, is
similarly deprecated in favor of `sloppy`.

<a id="DEP0066"></a>
