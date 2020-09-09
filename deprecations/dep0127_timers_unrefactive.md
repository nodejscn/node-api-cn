<!-- YAML
changes:
  - version: v11.14.0
    pr-url: https://github.com/nodejs/node/pull/26760
    description: Runtime deprecation.
-->

Type: Runtime

The previously undocumented and "private" `timers._unrefActive()` is deprecated.
Please use the publicly documented [`timeout.refresh()`][] instead.
If unreferencing the timeout is necessary, [`timeout.unref()`][] can be used
with no performance impact since Node.js 10.

