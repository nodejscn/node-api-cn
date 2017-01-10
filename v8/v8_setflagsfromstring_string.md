<!-- YAML
added: v1.0.0
-->

The `v8.setFlagsFromString()` method can be used to programmatically set
V8 command line flags. This method should be used with care. Changing settings
after the VM has started may result in unpredictable behavior, including
crashes and data loss; or it may simply do nothing.

The V8 options available for a version of Node.js may be determined by running
`node --v8-options`.  An unofficial, community-maintained list of options
and their effects is available [here][].

Usage:

```js
// Print GC events to stdout for one minute.
const v8 = require('v8');
v8.setFlagsFromString('--trace_gc');
setTimeout(function() { v8.setFlagsFromString('--notrace_gc'); }, 60e3);
```

[V8]: https://developers.google.com/v8/
[here]: https://github.com/thlorenz/v8-flags/blob/master/flags-0.11.md
[`GetHeapSpaceStatistics`]: https://v8docs.nodesource.com/node-5.0/d5/dda/classv8_1_1_isolate.html#ac673576f24fdc7a33378f8f57e1d13a4
