<!-- YAML
added: v15.0.0
-->

* `value` {any} A value with which the promise is fulfilled.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Immediate`
    should not require the Node.js event loop to remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Immediate`.

```mjs
import {
  setImmediate,
} from 'timers/promises';

const res = await setImmediate('result');

console.log(res);  // Prints 'result'
```

```cjs
const {
  setImmediate,
} = require('timers/promises');

setImmediate('result').then((res) => {
  console.log(res);  // Prints 'result'
});
```

