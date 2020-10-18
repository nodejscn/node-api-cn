<!-- YAML
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31165
    description: End-of-Life.
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.11.15
    pr-url: https://github.com/nodejs/node-v0.x-archive/pull/8826
    description: Runtime deprecation.
-->

Type: End-of-Life

The `_writableState.buffer` has been removed. Use `_writableState.getBuffer()`
instead.

