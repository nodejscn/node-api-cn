<!-- YAML
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15990
    description: Runtime deprecation.
-->

Type: Runtime

`fs.truncate()` `fs.truncateSync()` usage with a file descriptor is
deprecated. Please use `fs.ftruncate()` or `fs.ftruncateSync()` to work with
file descriptors.

