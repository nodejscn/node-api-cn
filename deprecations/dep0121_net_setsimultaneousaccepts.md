<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23760
    description: Runtime deprecation.
-->

Type: Runtime

The undocumented `net._setSimultaneousAccepts()` function was originally
intended for debugging and performance tuning when using the `child_process`
and `cluster` modules on Windows. The function is not generally useful and
is being removed. See discussion here:
<https://github.com/nodejs/node/issues/18391>

