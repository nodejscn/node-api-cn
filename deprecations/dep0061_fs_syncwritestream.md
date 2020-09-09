<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/20735
    description: End-of-Life.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10467
    description: Runtime deprecation.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/6749
    description: Documentation-only deprecation.
-->

Type: End-of-Life

The `fs.SyncWriteStream` class was never intended to be a publicly accessible
API and has been removed. No alternative API is available. Please use a userland
alternative.

