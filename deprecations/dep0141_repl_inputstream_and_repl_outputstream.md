<!-- YAML
changes:
  - version: v14.3.0
    pr-url: https://github.com/nodejs/node/pull/33294
    description: Documentation-only (supports [`--pending-deprecation`][]).
-->

Type: Documentation-only (supports [`--pending-deprecation`][])

The `repl` module exported the input and output stream twice. Use `.input`
instead of `.inputStream` and `.output` instead of `.outputStream`.

