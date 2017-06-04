<!-- YAML
added: v0.11.14
-->

> Stability: 0 - Deprecated. An alternative is in development.

* `code` {string} The JavaScript code to compile and run.

The `vm.runInDebugContext()` method compiles and executes `code` inside the V8
debug context. The primary use case is to gain access to the V8 `Debug` object:

```js
const vm = require('vm');
const Debug = vm.runInDebugContext('Debug');
console.log(Debug.findScript(process.emit).name);  // 'events.js'
console.log(Debug.findScript(process.exit).name);  // 'internal/process.js'
```

*Note*: The debug context and object are intrinsically tied to V8's debugger
implementation and may change (or even be removed) without prior warning.

The `Debug` object can also be made available using the V8-specific
`--expose_debug_as=` [command line option][].

