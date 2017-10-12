<!-- YAML
added: v8.5.0
-->
* `options` {Object}
  * `entryTypes` {Array} An array of strings identifying the types of
    `PerformanceEntry` instances the observer is interested in. If not
    provided an error will be thrown.
  * `buffered` {boolean} If true, the notification callback will be
    called using `setImmediate()` and multiple `PerformanceEntry` instance
    notifications will be buffered internally. If `false`, notifications will
    be immediate and synchronous. Defaults to `false`.

Subscribes the `PerformanceObserver` instance to notifications of new
`PerformanceEntry` instances identified by `options.entryTypes`.

When `options.buffered` is `false`, the `callback` will be invoked once for
every `PerformanceEntry` instance:

```js
const {
  performance,
  PerformanceObserver
} = require('perf_hooks');

const obs = new PerformanceObserver((list, observer) => {
  // called three times synchronously. list contains one item
});
obs.observe({ entryTypes: ['mark'] });

for (let n = 0; n < 3; n++)
  performance.mark(`test${n}`);
```

```js
const {
  performance,
  PerformanceObserver
} = require('perf_hooks');

const obs = new PerformanceObserver((list, observer) => {
  // called once. list contains three items
});
obs.observe({ entryTypes: ['mark'], buffered: true });

for (let n = 0; n < 3; n++)
  performance.mark(`test${n}`);
```

