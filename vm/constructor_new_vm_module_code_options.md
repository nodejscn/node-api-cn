
* `code` {string} JavaScript Module code to parse
* `options`
  * `url` {string} URL used in module resolution and stack traces. **Default:**
    `'vm:module(i)'` where `i` is a context-specific ascending index.
  * `context` {Object} The [contextified][] object as returned by the
    `vm.createContext()` method, to compile and evaluate this `Module` in.
  * `lineOffset` {integer} Specifies the line number offset that is displayed
    in stack traces produced by this `Module`.
  * `columnOffset` {integer} Specifies the column number offset that is
    displayed in stack traces produced by this `Module`.
  * `initalizeImportMeta` {Function} Called during evaluation of this `Module`
    to initialize the `import.meta`. This function has the signature `(meta,
    module)`, where `meta` is the `import.meta` object in the `Module`, and
    `module` is this `vm.Module` object.

Creates a new ES `Module` object.

*Note*: Properties assigned to the `import.meta` object that are objects may
allow the `Module` to access information outside the specified `context`, if the
object is created in the top level context. Use `vm.runInContext()` to create
objects in a specific context.

```js
const vm = require('vm');

const contextifiedSandbox = vm.createContext({ secret: 42 });

(async () => {
  const module = new vm.Module(
    'Object.getPrototypeOf(import.meta.prop).secret = secret;',
    {
      initializeImportMeta(meta) {
        // Note: this object is created in the top context. As such,
        // Object.getPrototypeOf(import.meta.prop) points to the
        // Object.prototype in the top context rather than that in
        // the sandbox.
        meta.prop = {};
      }
    });
  // Since module has no dependencies, the linker function will never be called.
  await module.link(() => {});
  module.initialize();
  await module.evaluate();

  // Now, Object.prototype.secret will be equal to 42.
  //
  // To fix this problem, replace
  //     meta.prop = {};
  // above with
  //     meta.prop = vm.runInContext('{}', contextifiedSandbox);
})();
```

