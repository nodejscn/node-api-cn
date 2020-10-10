<!-- YAML
changes:
  - version: v14.3.0
    pr-url: https://github.com/nodejs/node/pull/33294
    description: Documentation-only (supports [`--pending-deprecation`][]).
-->

Type: Documentation-only

The `repl` module exports a `_builtinLibs` property that contains an array with
native modules. It was incomplete so far and instead it's better to rely upon
`require('module').builtinModules`.

