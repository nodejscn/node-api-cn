
The following example measures the duration of `require()` operations to load
dependencies:

<!-- eslint-disable no-global-assign -->
```js
'use strict';
const {
  performance,
  PerformanceObserver
} = require('perf_hooks');
const mod = require('module');

// Monkey patch the require function
mod.Module.prototype.require =
  performance.timerify(mod.Module.prototype.require);
require = performance.timerify(require);

// Activate the observer
const obs = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach((entry) => {
    console.log(`require('${entry[0]}')`, entry.duration);
  });
  obs.disconnect();
  // Free memory
  performance.clearFunctions();
});
obs.observe({ entryTypes: ['function'], buffered: true });

require('some-module');
```

[`timeOrigin`]: https://w3c.github.io/hr-time/#dom-performance-timeorigin
[Async Hooks]: async_hooks.html
[W3C Performance Timeline]: https://w3c.github.io/performance-timeline/
