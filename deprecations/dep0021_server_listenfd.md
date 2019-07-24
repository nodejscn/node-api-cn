<!-- YAML
changes:
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.7.12
    commit: 41421ff9da1288aa241a5e9dcf915b685ade1c23
    description: Runtime deprecation.
-->

Type: Runtime

The `Server.listenFD()` method is deprecated. Please use
[`Server.listen({fd: <number>})`][] instead.

<a id="DEP0022"></a>
