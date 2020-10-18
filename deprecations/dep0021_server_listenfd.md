<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27127
    description: End-of-Life.
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.7.12
    commit: 41421ff9da1288aa241a5e9dcf915b685ade1c23
    description: Runtime deprecation.
-->

Type: End-of-Life

The `Server.listenFD()` method was deprecated and removed. Please use
[`Server.listen({fd: <number>})`][] instead.

