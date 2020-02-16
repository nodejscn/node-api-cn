
The most straightforward `package.json` would be one that defines the separate
CommonJS and ES module entry points directly:

<!-- eslint-skip -->
```js
// ./node_modules/pkg/package.json
{
  "type": "module",
  "main": "./index.cjs",
  "exports": {
    "import": "./index.mjs",
    "require": "./index.cjs"
  }
}
```

This can be done if both the CommonJS and ES module versions of the package are
equivalent, for example because one is the transpiled output of the other; and
the package’s management of state is carefully isolated (or the package is
stateless).

The reason that state is an issue is because both the CommonJS and ES module
versions of the package may get used within an application; for example, the
user’s application code could `import` the ES module version while a dependency
`require`s the CommonJS version. If that were to occur, two copies of the
package would be loaded in memory and therefore two separate states would be
present. This would likely cause hard-to-troubleshoot bugs.

Aside from writing a stateless package (if JavaScript’s `Math` were a package,
for example, it would be stateless as all of its methods are static), there are
some ways to isolate state so that it’s shared between the potentially loaded
CommonJS and ES module instances of the package:

1. If possible, contain all state within an instantiated object. JavaScript’s
   `Date`, for example, needs to be instantiated to contain state; if it were a
   package, it would be used like this:

    ```js
    import Date from 'date';
    const someDate = new Date();
    // someDate contains state; Date does not
    ```

   The `new` keyword isn’t required; a package’s function can return a new
   object, or modify a passed-in object, to keep the state external to the
   package.

1. Isolate the state in one or more CommonJS files that are shared between the
   CommonJS and ES module versions of the package. For example, if the CommonJS
   and ES module entry points are `index.cjs` and `index.mjs`, respectively:

    ```js
    // ./node_modules/pkg/index.cjs
    const state = require('./state.cjs');
    module.exports.state = state;
    ```

    ```js
    // ./node_modules/pkg/index.mjs
    import state from './state.cjs';
    export {
      state
    };
    ```

   Even if `pkg` is used via both `require` and `import` in an application (for
   example, via `import` in application code and via `require` by a dependency)
   each reference of `pkg` will contain the same state; and modifying that
   state from either module system will apply to both.

Any plugins that attach to the package’s singleton would need to separately
attach to both the CommonJS and ES module singletons.

This approach is appropriate for any of the following use cases:
* The package is currently written in ES module syntax and the package author
  wants that version to be used wherever such syntax is supported.
* The package is stateless or its state can be isolated without too much
  difficulty.
* The package is unlikely to have other public packages that depend on it, or if
  it does, the package is stateless or has state that need not be shared between
  dependencies or with the overall application.

Even with isolated state, there is still the cost of possible extra code
execution between the CommonJS and ES module versions of a package.

As with the previous approach, a variant of this approach not requiring
conditional exports for consumers could be to add an export, e.g.
`"./module"`, to point to an all-ES module-syntax version of the package:

<!-- eslint-skip -->
```js
// ./node_modules/pkg/package.json
{
  "type": "module",
  "main": "./index.cjs",
  "exports": {
    ".": "./index.cjs",
    "./module": "./index.mjs"
  }
}
```

