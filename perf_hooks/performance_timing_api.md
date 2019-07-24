
<!--introduced_in=v8.5.0-->

> Stability: 1 - Experimental

The Performance Timing API provides an implementation of the
[W3C Performance Timeline][] specification. The purpose of the API
is to support collection of high resolution performance metrics.
This is the same Performance API as implemented in modern Web browsers.

```js
const { PerformanceObserver, performance } = require('perf_hooks');

const obs = new PerformanceObserver((items) => {
  console.log(items.getEntries()[0].duration);
  performance.clearMarks();
});
obs.observe({ entryTypes: ['measure'] });

performance.mark('A');
doSomeLongRunningProcess(() => {
  performance.mark('B');
  performance.measure('A to B', 'A', 'B');
});
```

