
<!--introduced_in=v8.5.0-->

> Stability: 2 - Stable

<!-- source_link=lib/perf_hooks.js -->

This module provides an implementation of a subset of the W3C
[Web Performance APIs][] as well as additional APIs for
Node.js-specific performance measurements.

Node.js supports the following [Web Performance APIs][]:

* [High Resolution Time][]
* [Performance Timeline][]
* [User Timing][]

```js
const { PerformanceObserver, performance } = require('perf_hooks');

const obs = new PerformanceObserver((items) => {
  console.log(items.getEntries()[0].duration);
  performance.clearMarks();
});
obs.observe({ type: 'measure' });
performance.measure('Start to Now');

performance.mark('A');
doSomeLongRunningProcess(() => {
  performance.measure('A to Now', 'A');

  performance.mark('B');
  performance.measure('A to B', 'A', 'B');
});
```

