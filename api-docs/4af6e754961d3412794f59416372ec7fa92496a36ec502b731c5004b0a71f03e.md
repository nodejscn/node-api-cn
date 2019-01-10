
* `linker` {Function}
* Returns: {Promise}

Link module dependencies. This method must be called before instantiation, and
can only be called once per module.

Two parameters will be passed to the `linker` function:

- `specifier` The specifier of the requested module:
  <!-- eslint-skip -->
  ```js
  import foo from 'foo';
  //              ^^^^^ the module specifier
  ```
- `referencingModule` The `Module` object `link()` is called on.

The function is expected to return a `Module` object or a `Promise` that
eventually resolves to a `Module` object. The returned `Module` must satisfy the
following two invariants:

- It must belong to the same context as the parent `Module`.
- Its `linkingStatus` must not be `'errored'`.

If the returned `Module`'s `linkingStatus` is `'unlinked'`, this method will be
recursively called on the returned `Module` with the same provided `linker`
function.

`link()` returns a `Promise` that will either get resolved when all linking
instances resolve to a valid `Module`, or rejected if the linker function either
throws an exception or returns an invalid `Module`.

The linker function roughly corresponds to the implementation-defined
[HostResolveImportedModule][] abstract operation in the ECMAScript
specification, with a few key differences:

- The linker function is allowed to be asynchronous while
  [HostResolveImportedModule][] is synchronous.
- The linker function is executed during linking, a Node.js-specific stage
  before instantiation, while [HostResolveImportedModule][] is called during
  instantiation.

The actual [HostResolveImportedModule][] implementation used during module
instantiation is one that returns the modules linked during linking. Since at
that point all modules would have been fully linked already, the
[HostResolveImportedModule][] implementation is fully synchronous per
specification.

