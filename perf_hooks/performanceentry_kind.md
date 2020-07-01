<!-- YAML
added: v8.5.0
-->

* {number}

_This property is an extension by Node.js. It is not available in Web browsers._

When `performanceEntry.entryType` is equal to `'gc'`, the `performance.kind`
property identifies the type of garbage collection operation that occurred.
The value may be one of:

* `perf_hooks.constants.NODE_PERFORMANCE_GC_MAJOR`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_MINOR`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_INCREMENTAL`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_WEAKCB`

