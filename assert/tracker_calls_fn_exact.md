<!-- YAML
added: v14.2.0
-->

* `fn` {Function} **Default** A no-op function.
* `exact` {number} **Default** `1`.
* Returns: {Function} that wraps `fn`.

The wrapper function is expected to be called exactly `exact` times. If the
function has not been called exactly `exact` times when
[`tracker.verify()`][] is called, then [`tracker.verify()`][] will throw an
error.

```js
const assert = require('assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func);
```

