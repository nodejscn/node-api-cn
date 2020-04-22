<!-- YAML
added: v13.0.0
-->

> Stability: 1 - Experimental

*This feature is only available with the `--experimental-vm-modules` command
flag enabled.*

The `vm.Module` class provides a low-level interface for using
ECMAScript modules in VM contexts. It is the counterpart of the `vm.Script`
class that closely mirrors [Module Record][]s as defined in the ECMAScript
specification.

Unlike `vm.Script` however, every `vm.Module` object is bound to a context from
its creation. Operations on `vm.Module` objects are intrinsically asynchronous,
in contrast with the synchronous nature of `vm.Script` objects. The use of
'async' functions can help with manipulating `vm.Module` objects.

Using a `vm.Module` object requires three distinct steps: creation/parsing,
linking, and evaluation. These three steps are illustrated in the following
example.

This implementation lies at a lower level than the [ECMAScript Module
loader][]. There is also currently no way to interact with the Loader, though
support is planned.

```js
const vm = require('vm');

const contextifiedObject = vm.createContext({ secret: 42 });

(async () => {
  // Step 1
  //
  // Create a Module by constructing a new `vm.SourceTextModule` object. This
  // parses the provided source text, throwing a `SyntaxError` if anything goes
  // wrong. By default, a Module is created in the top context. But here, we
  // specify `contextifiedObject` as the context this Module belongs to.
  //
  // Here, we attempt to obtain the default export from the module "foo", and
  // put it into local binding "secret".

  const bar = new vm.SourceTextModule(`
    import s from 'foo';
    s;
  `, { context: contextifiedObject });

  // Step 2
  //
  // "Link" the imported dependencies of this Module to it.
  //
  // The provided linking callback (the "linker") accepts two arguments: the
  // parent module (`bar` in this case) and the string that is the specifier of
  // the imported module. The callback is expected to return a Module that
  // corresponds to the provided specifier, with certain requirements documented
  // in `module.link()`.
  //
  // If linking has not started for the returned Module, the same linker
  // callback will be called on the returned Module.
  //
  // Even top-level Modules without dependencies must be explicitly linked. The
  // callback provided would never be called, however.
  //
  // The link() method returns a Promise that will be resolved when all the
  // Promises returned by the linker resolve.
  //
  // Note: This is a contrived example in that the linker function creates a new
  // "foo" module every time it is called. In a full-fledged module system, a
  // cache would probably be used to avoid duplicated modules.

  async function linker(specifier, referencingModule) {
    if (specifier === 'foo') {
      return new vm.SourceTextModule(`
        // The "secret" variable refers to the global variable we added to
        // "contextifiedObject" when creating the context.
        export default secret;
      `, { context: referencingModule.context });

      // Using `contextifiedObject` instead of `referencingModule.context`
      // here would work as well.
    }
    throw new Error(`Unable to resolve dependency: ${specifier}`);
  }
  await bar.link(linker);

  // Step 3
  //
  // Evaluate the Module. The evaluate() method returns a Promise with a single
  // property "result" that contains the result of the very last statement
  // executed in the Module. In the case of `bar`, it is `s;`, which refers to
  // the default export of the `foo` module, the `secret` we set in the
  // beginning to 42.

  const { result } = await bar.evaluate();

  console.log(result);
  // Prints 42.
})();
```

