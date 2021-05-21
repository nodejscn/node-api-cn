<!-- YAML
added: v15.0.0
-->

* `delay` {number} The number of milliseconds to wait before fulfilling the
  promise. **Default:** `1`.
* `value` {any} A value with which the promise is fulfilled.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Timeout`
    should not require the Node.js event loop to remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Timeout`.

```mjs
import {
  setTimeout,
} from 'timers/promises';

const res = await setTimeout(100, 'result');

console.log(res);  // Prints 'result'
```

```cjs
const {
  setTimeout,
} = require('timers/promises');

setTimeout(100, 'result').then((res) => {
  console.log(res);  // Prints 'result'
});
```

