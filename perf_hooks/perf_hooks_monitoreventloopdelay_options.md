<!-- YAML
added: v11.10.0
-->

* `options` {Object}
  * `resolution` {number} The sampling rate in milliseconds. Must be greater
    than zero. **Default:** `10`.
* Returns: {Histogram}

_This property is an extension by Node.js. It is not available in Web browsers._

Creates a `Histogram` object that samples and reports the event loop delay
over time. The delays will be reported in nanoseconds.

Using a timer to detect approximate event loop delay works because the
execution of timers is tied specifically to the lifecycle of the libuv
event loop. That is, a delay in the loop will cause a delay in the execution
of the timer, and those delays are specifically what this API is intended to
detect.

```js
const { monitorEventLoopDelay } = require('perf_hooks');
const h = monitorEventLoopDelay({ resolution: 20 });
h.enable();
// Do something.
h.disable();
console.log(h.min);
console.log(h.max);
console.log(h.mean);
console.log(h.stddev);
console.log(h.percentiles);
console.log(h.percentile(50));
console.log(h.percentile(99));
```

