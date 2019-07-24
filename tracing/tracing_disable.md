<!-- YAML
added: v10.0.0
-->

Disables this `Tracing` object.

Only trace event categories *not* covered by other enabled `Tracing` objects
and *not* specified by the `--trace-event-categories` flag will be disabled.

```js
const trace_events = require('trace_events');
const t1 = trace_events.createTracing({ categories: ['node', 'v8'] });
const t2 = trace_events.createTracing({ categories: ['node.perf', 'node'] });
t1.enable();
t2.enable();

// Prints 'node,node.perf,v8'
console.log(trace_events.getEnabledCategories());

t2.disable(); // Will only disable emission of the 'node.perf' category

// Prints 'node,v8'
console.log(trace_events.getEnabledCategories());
```

