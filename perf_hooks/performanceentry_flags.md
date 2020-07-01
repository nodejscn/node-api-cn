<!-- YAML
added: v13.9.0
-->

* {number}

_This property is an extension by Node.js. It is not available in Web browsers._

When `performanceEntry.entryType` is equal to `'gc'`, the `performance.flags`
property contains additional information about garbage collection operation.
The value may be one of:

* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_NO`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_CONSTRUCT_RETAINED`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_FORCED`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_SYNCHRONOUS_PHANTOM_PROCESSING`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_ALL_AVAILABLE_GARBAGE`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_ALL_EXTERNAL_MEMORY`
* `perf_hooks.constants.NODE_PERFORMANCE_GC_FLAGS_SCHEDULE_IDLE`

