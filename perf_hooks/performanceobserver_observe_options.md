<!-- YAML
added: v8.5.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37136
    description: Updated to conform to User Timing Level 3. The
                 buffered option has been removed.
-->

* `options` {Object}
  * `type` {string} A single {PerformanceEntry} type. Must not be given
    if `entryTypes` is already specified.
  * `entryTypes` {string[]} An array of strings identifying the types of
    {PerformanceEntry} instances the observer is interested in. If not
    provided an error will be thrown.

Subscribes the {PerformanceObserver} instance to notifications of new
{PerformanceEntry} instances identified either by `options.entryTypes`
or `options.type`:

```js
const {
  performance,
  PerformanceObserver
} = require('perf_hooks');

const obs = new PerformanceObserver((list, observer) => {
  // Called three times synchronously. `list` contains one item.
});
obs.observe({ type: 'mark' });

for (let n = 0; n < 3; n++)
  performance.mark(`test${n}`);
```

