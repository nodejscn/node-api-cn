
* `code` {string} JavaScript Module code to parse
* `options`
  * `url` {string} URL used in module resolution and stack traces. **Default:**
    `'vm:module(i)'` where `i` is a context-specific ascending index.
  * `context` {Object} The [contextified][] object as returned by the
    `vm.createContext()` method, to compile and evaluate this `Module` in.
  * `lineOffset` {integer} Specifies the line number offset that is displayed
    in stack traces produced by this `Module`. **Default:** `0`.
  * `columnOffset` {integer} Specifies the column number offset that is
    displayed in stack traces produced by this `Module`. **Default:** `0`.
  * `initializeImportMeta` {Function} Called during evaluation of this `Module`
    to initialize the `import.meta`.
    * `meta` {import.meta}
    * `module` {vm.SourceTextModule}
  * `importModuleDynamically` {Function} Called during evaluation of this module
    when `import()` is called. If this option is not specified, calls to
    `import()` will reject with [`ERR_VM_DYNAMIC_IMPORT_CALLBACK_MISSING`][].
    * `specifier` {string} specifier passed to `import()`
    * `module` {vm.SourceTextModule}
    * Returns: {Module Namespace Object|vm.SourceTextModule} Returning a
      `vm.SourceTextModule` is recommended in order to take advantage of error
      tracking, and to avoid issues with namespaces that contain `then`
      function exports.

Creates a new ES `Module` object.

Properties assigned to the `import.meta` object that are objects may
allow the `Module` to access information outside the specified `context`, if the
object is created in the top level context. Use `vm.runInContext()` to create
objects in a specific context.

```js
const vm = require('vm');

const contextifiedSandbox = vm.createContext({ secret: 42 });

(async () => {
  const module = new vm.SourceTextModule(
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
  module.instantiate();
  await module.evaluate();

  // Now, Object.prototype.secret will be equal to 42.
  //
  // To fix this problem, replace
  //     meta.prop = {};
  // above with
  //     meta.prop = vm.runInContext('{}', contextifiedSandbox);
})();
```

