<!-- YAML
added: v8.5.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37475
    description: Added the histogram option.
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37136
    description: Re-implemented to use pure-JavaScript and the ability
                 to time async functions.
-->

* `fn` {Function}
* `options` {Object}
  * `histogram` {RecordableHistogram} A histogram object created using
    `perf_hooks.createHistogram()` that will record runtime durations in
    nanoseconds.

_This property is an extension by Node.js. It is not available in Web browsers._

Wraps a function within a new function that measures the running time of the
wrapped function. A `PerformanceObserver` must be subscribed to the `'function'`
event type in order for the timing details to be accessed.

```js
const {
  performance,
  PerformanceObserver
} = require('perf_hooks');

function someFunction() {
  console.log('hello world');
}

const wrapped = performance.timerify(someFunction);

const obs = new PerformanceObserver((list) => {
  console.log(list.getEntries()[0].duration);
  obs.disconnect();
});
obs.observe({ entryTypes: ['function'] });

// A performance timeline entry will be created
wrapped();
```

If the wrapped function returns a promise, a finally handler will be attached
to the promise and the duration will be reported once the finally handler is
invoked.

