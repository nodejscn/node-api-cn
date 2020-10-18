<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17147
    description: End-of-Life.
  - version:
    - v9.4.0
    - v8.10.0
    pr-url: https://github.com/nodejs/node/pull/16972
    description: Runtime deprecation.
-->

Type: End-of-Life

The AsyncHooks sensitive API was never documented and had various minor issues.
Use the `AsyncResource` API instead. See
<https://github.com/nodejs/node/issues/15572>.

