<!-- YAML
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/33648
    description: The legacy `node debug` command was removed.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11441
    description: Runtime deprecation.
-->

Type: End-of-Life

`node debug` corresponds to the legacy CLI debugger which has been replaced with
a V8-inspector based CLI debugger available through `node inspect`.

