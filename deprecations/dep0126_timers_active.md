<!-- YAML
changes:
  - version: v11.14.0
    pr-url: https://github.com/nodejs/node/pull/26760
    description: Runtime deprecation.
-->

Type: Runtime

The previously undocumented `timers.active()` is deprecated.
Please use the publicly documented [`timeout.refresh()`][] instead.
If re-referencing the timeout is necessary, [`timeout.ref()`][] can be used
with no performance impact since Node.js 10.

