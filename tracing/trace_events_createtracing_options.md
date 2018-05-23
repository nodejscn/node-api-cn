<!-- YAML
added: v10.0.0
-->

* `options` {Object}
  * `categories` {string[]} An array of trace category names. Values included
    in the array are coerced to a string when possible. An error will be
    thrown if the value cannot be coerced.
* Returns: {Tracing}.

Creates and returns a `Tracing` object for the given set of `categories`.

```js
const trace_events = require('trace_events');
const categories = ['node.perf', 'node.async_hooks'];
const tracing = trace_events.createTracing({ categories });
tracing.enable();
// do stuff
tracing.disable();
```

