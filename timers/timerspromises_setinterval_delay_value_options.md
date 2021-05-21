<!-- YAML
added: v15.9.0
-->

Returns an async iterator that generates values in an interval of `delay` ms.

* `delay` {number} The number of milliseconds to wait between iterations.
   **Default:** `1`.
* `value` {any} A value with which the iterator returns.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Timeout`
    between iterations should not require the Node.js event loop to
    remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Timeout` between operations.

```mjs
import {
  setInterval,
} from 'timers/promises';

const interval = 100;
for await (const startTime of setInterval(interval, Date.now())) {
  const now = Date.now();
  console.log(now);
  if ((now - startTime) > 1000)
    break;
}
console.log(Date.now());
```

```cjs
const {
  setInterval,
} = require('timers/promises');
const interval = 100;

(async function() {
  for await (const startTime of setInterval(interval, Date.now())) {
    const now = Date.now();
    console.log(now);
    if ((now - startTime) > 1000)
      break;
  }
  console.log(Date.now());
})();
```












