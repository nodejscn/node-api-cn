<!-- YAML
added: v14.10.0
-->

* `util1` {Object} The result of a previous call to `eventLoopUtilization()`
* `util2` {Object} The result of a previous call to `eventLoopUtilization()`
    prior to `util1`
* Returns {Object}
  * `idle` {number}
  * `active` {number}
  * `utilization` {number}

The `eventLoopUtilization()` method returns an object that contains the
cumulative duration of time the event loop has been both idle and active as a
high resolution milliseconds timer. The `utilization` value is the calculated
Event Loop Utilization (ELU). If bootstrapping has not yet finished, the
properties have the value of 0.

`util1` and `util2` are optional parameters.

If `util1` is passed then the delta between the current call's `active` and
`idle` times are calculated and returned (similar to [`process.hrtime()`][]).
Likewise the adjusted `utilization` value is calculated.

If `util1` and `util2` are both passed then the calculation adjustments are
done between the two arguments. This is a convenience option because unlike
[`process.hrtime()`][] additional work is done to calculate the ELU.

ELU is similar to CPU utilization except that it is calculated using high
precision wall-clock time. It represents the percentage of time the event loop
has spent outside the event loop's event provider (e.g. `epoll_wait`). No other
CPU idle time is taken into consideration. The following is an example of how
a mostly idle process will have a high ELU.

<!-- eslint-skip -->
```js
'use strict';
const { eventLoopUtilization } = require('perf_hooks').performance;
const { spawnSync } = require('child_process');

setImmediate(() => {
  const elu = eventLoopUtilization();
  spawnSync('sleep', ['5']);
  console.log(eventLoopUtilization(elu).utilization);
});
```

While the CPU is mostly idle while running this script the value of
`utilization` is 1. This is because the call to [`child_process.spawnSync()`][]
blocks the event loop from proceeding.

Passing in a user-defined object instead of the result of a previous call to
`eventLoopUtilization()` will lead to undefined behavior. The return values
are not guaranteed to reflect any correct state of the event loop.

