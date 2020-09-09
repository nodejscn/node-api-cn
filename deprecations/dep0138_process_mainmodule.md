<!-- YAML
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/32232
    description: Documentation-only deprecation.
-->

Type: Documentation-only

[`process.mainModule`][] is a CommonJS-only feature while `process` global
object is shared with non-CommonJS environment. Its use within ECMAScript
modules is unsupported.

It is deprecated in favor of [`require.main`][], because it serves the same
purpose and is only available on CommonJS environment.

