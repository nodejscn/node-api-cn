<!-- YAML
added: v0.1.16
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/12794
    description: Added support for the `flags` argument.
-->

* `module` {Object}
* `filename` {string}
* `flags` {os.constants.dlopen} **Default:** `os.constants.dlopen.RTLD_LAZY`

The `process.dlopen()` method allows to dynamically load shared
objects. It is primarily used by `require()` to load
C++ Addons, and should not be used directly, except in special
cases. In other words, [`require()`][] should be preferred over
`process.dlopen()`, unless there are specific reasons.

The `flags` argument is an integer that allows to specify dlopen
behavior. See the [`os.constants.dlopen`][] documentation for details.

If there are specific reasons to use `process.dlopen()` (for instance,
to specify dlopen flags), it's often useful to use [`require.resolve()`][]
to look up the module's path.

An important drawback when calling `process.dlopen()` is that the `module`
instance must be passed. Functions exported by the C++ Addon will be accessible
via `module.exports`.

The example below shows how to load a C++ Addon, named as `binding`,
that exports a `foo` function. All the symbols will be loaded before
the call returns, by passing the `RTLD_NOW` constant. In this example
the constant is assumed to be available.

```js
const os = require('os');
process.dlopen(module, require.resolve('binding'),
               os.constants.dlopen.RTLD_NOW);
module.exports.foo();
```

