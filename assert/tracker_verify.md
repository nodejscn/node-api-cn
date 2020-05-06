<!-- YAML
added: v14.2.0
-->

Iterates through the list of functions passed to
[`tracker.calls()`][] and will throw an error for functions that
have not been called the expected number of times.

```js
const assert = require('assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

callsfunc();

// Will throw an error since callsfunc() was only called once.
tracker.verify();
```

