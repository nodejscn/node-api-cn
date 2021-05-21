<!-- YAML
added:
  - v14.2.0
  - v12.19.0
-->

* Returns: {Array} of objects containing information about the wrapper functions
  returned by [`tracker.calls()`][].
* Object {Object}
  * `message` {string}
  * `actual` {number} The actual number of times the function was called.
  * `expected` {number} The number of times the function was expected to be
    called.
  * `operator` {string} The name of the function that is wrapped.
  * `stack` {Object} A stack trace of the function.

The arrays contains information about the expected and actual number of calls of
the functions that have not been called the expected number of times.

```mjs
import assert from 'assert';

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

function foo() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

// Returns an array containing information on callsfunc()
tracker.report();
// [
//  {
//    message: 'Expected the func function to be executed 2 time(s) but was
//    executed 0 time(s).',
//    actual: 0,
//    expected: 2,
//    operator: 'func',
//    stack: stack trace
//  }
// ]
```

```cjs
const assert = require('assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

function foo() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

// Returns an array containing information on callsfunc()
tracker.report();
// [
//  {
//    message: 'Expected the func function to be executed 2 time(s) but was
//    executed 0 time(s).',
//    actual: 0,
//    expected: 2,
//    operator: 'func',
//    stack: stack trace
//  }
// ]
```

