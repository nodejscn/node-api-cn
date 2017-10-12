<!-- YAML
added: v8.5.0
-->

> Stability: 1 - Experimental

The Performance Timing API provides an implementation of the
[W3C Performance Timeline][] specification. The purpose of the API
is to support collection of high resolution performance metrics.
This is the same Performance API as implemented in modern Web browsers.

```js
const { performance } = require('perf_hooks');
performance.mark('A');
doSomeLongRunningProcess(() => {
  performance.mark('B');
  performance.measure('A to B', 'A', 'B');
  const measure = performance.getEntriesByName('A to B')[0];
  console.log(measure.duration);
  // Prints the number of milliseconds between Mark 'A' and Mark 'B'
});
```

