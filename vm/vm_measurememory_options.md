
<!-- YAML
added: v13.10.0
-->

> Stability: 1 - Experimental

Measure the memory known to V8 and used by the current execution context
or a specified context.

* `options` {Object} Optional.
  * `mode` {string} Either `'summary'` or `'detailed'`.
    **Default:** `'summary'`
  * `context` {Object} Optional. A [contextified][] object returned
    by `vm.createContext()`. If not specified, measure the memory
    usage of the current context where `vm.measureMemory()` is invoked.
* Returns: {Promise} If the memory is successfully measured the promise will
  resolve with an object containing information about the memory usage.

The format of the object that the returned Promise may resolve with is
specific to the V8 engine and may change from one version of V8 to the next.

The returned result is different from the statistics returned by
`v8.getHeapSpaceStatistics()` in that `vm.measureMemory()` measures
the memory reachable by V8 from a specific context, while
`v8.getHeapSpaceStatistics()` measures the memory used by an instance
of V8 engine, which can switch among multiple contexts that reference
objects in the heap of one engine.

```js
const vm = require('vm');
// Measure the memory used by the current context and return the result
// in summary.
vm.measureMemory({ mode: 'summary' })
  // Is the same as vm.measureMemory()
  .then((result) => {
    // The current format is:
    // { total: { jsMemoryEstimate: 2211728, jsMemoryRange: [ 0, 2211728 ] } }
    console.log(result);
  });

const context = vm.createContext({});
vm.measureMemory({ mode: 'detailed' }, context)
  .then((result) => {
    // At the moment the detailed format is the same as the summary one.
    console.log(result);
  });
```

