<!-- YAML
added: v12.12.0
changes:
  - version: v15.11.0
    pr-url: https://github.com/nodejs/node/pull/37362
    description: This API is no longer experimental.
-->

Enable [Source Map v3][Source Map] support for stack traces.

When using a transpiler, such as TypeScript, stack traces thrown by an
application reference the transpiled code, not the original source position.
`--enable-source-maps` enables caching of Source Maps and makes a best
effort to report stack traces relative to the original source file.

Overriding `Error.prepareStackTrace` prevents `--enable-source-maps` from
modifying the stack trace.

