<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10970
    description: Runtime deprecation.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/25828
    description: End-of-Life.
-->

Type: End-of-Life

`--debug` activates the legacy V8 debugger interface, which was removed as
of V8 5.8. It is replaced by Inspector which is activated with `--inspect`
instead.

<a id="DEP0063"></a>
