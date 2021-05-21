<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/36902
    description: Runtime deprecation.
-->

Type: Runtime

The `process.config` property is intended to provide access to configuration
settings set when the Node.js binary was compiled. However, the property has
been mutable by user code making it impossible to rely on. The ability to
change the value has been deprecated and will be disabled in the future.

