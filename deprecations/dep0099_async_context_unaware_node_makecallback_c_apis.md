<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18632
    description: Compile-time deprecation.
-->

Type: Compile-time

Certain versions of `node::MakeCallback` APIs available to native modules are
deprecated. Please use the versions of the API that accept an `async_context`
parameter.

