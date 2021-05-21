
* `code` {string} JavaScript Module code to parse
* `options`
  * `identifier` {string} String used in stack traces.
    **Default:** `'vm:module(i)'` where `i` is a context-specific ascending
    index.
  * `cachedData` {Buffer|TypedArray|DataView} Provides an optional `Buffer` or
    `TypedArray`, or `DataView` with V8's code cache data for the supplied
     source. The `code` must be the same as the module from which this
     `cachedData` was created.
  * `context` {Object} The [contextified][] object as returned by the
    `vm.createContext()` method, to compile and evaluate this `Module` in.
  * `lineOffset` {integer} Specifies the line number offset that is displayed
    in stack traces produced by this `Module`. **Default:** `0`.
  * `columnOffset` {integer} Specifies the first-line column number offset that
    is displayed in stack traces produced by this `Module`. **Default:** `0`.
  * `initializeImportMeta` {Function} Called during evaluation of this `Module`
    to initialize the `import.meta`.
    * `meta` {import.meta}
    * `module` {vm.SourceTextModule}
  * `importModuleDynamically` {Function} Called during evaluation of this module
    when `import()` is called. If this option is not specified, calls to
    `import()` will reject with [`ERR_VM_DYNAMIC_IMPORT_CALLBACK_MISSING`][].
    * `specifier` {string} specifier passed to `import()`
    * `module` {vm.Module}
    * Returns: {Module Namespace Object|vm.Module} Returning a `vm.Module` is
      recommended in order to take advantage of error tracking, and to avoid
      issues with namespaces that contain `then` function exports.

Creates a new `SourceTextModule` instance.

Properties assigned to the `import.meta` object that are objects may
allow the module to access information outside the specified `context`. Use
`vm.runInContext()` to create objects in a specific context.

```mjs
import vm from 'vm';

const contextifiedObject = vm.createContext({ secret: 42 });

const module = new vm.SourceTextModule(
  'Object.getPrototypeOf(import.meta.prop).secret = secret;',
  {
    initializeImportMeta(meta) {
      // Note: this object is created in the top context. As such,
      // Object.getPrototypeOf(import.meta.prop) points to the
      // Object.prototype in the top context rather than that in
      // the contextified object.
      meta.prop = {};
    }
  });
// Since module has no dependencies, the linker function will never be called.
await module.link(() => {});
await module.evaluate();

// Now, Object.prototype.secret will be equal to 42.
//
// To fix this problem, replace
//     meta.prop = {};
// above with
//     meta.prop = vm.runInContext('{}', contextifiedObject);
```

```cjs
const vm = require('vm');
const contextifiedObject = vm.createContext({ secret: 42 });
(async () => {
  const module = new vm.SourceTextModule(
    'Object.getPrototypeOf(import.meta.prop).secret = secret;',
    {
      initializeImportMeta(meta) {
        // Note: this object is created in the top context. As such,
        // Object.getPrototypeOf(import.meta.prop) points to the
        // Object.prototype in the top context rather than that in
        // the contextified object.
        meta.prop = {};
      }
    });
  // Since module has no dependencies, the linker function will never be called.
  await module.link(() => {});
  await module.evaluate();
  // Now, Object.prototype.secret will be equal to 42.
  //
  // To fix this problem, replace
  //     meta.prop = {};
  // above with
  //     meta.prop = vm.runInContext('{}', contextifiedObject);
})();
```

