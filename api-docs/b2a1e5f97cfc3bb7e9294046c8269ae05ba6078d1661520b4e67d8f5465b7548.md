<!-- YAML
added: v0.3.1
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19398
    description: The `sandbox` option can no longer be a function.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19016
    description: The `codeGeneration` option is supported now.
-->

* `sandbox` {Object}
* `options` {Object}
  * `name` {string} Human-readable name of the newly created context.
    **Default:** `'VM Context i'`, where `i` is an ascending numerical index of
    the created context.
  * `origin` {string} [Origin][origin] corresponding to the newly created
    context for display purposes. The origin should be formatted like a URL,
    but with only the scheme, host, and port (if necessary), like the value of
    the [`url.origin`][] property of a [`URL`][] object. Most notably, this
    string should omit the trailing slash, as that denotes a path.
    **Default:** `''`.
  * `codeGeneration` {Object}
    * `strings` {boolean} If set to false any calls to `eval` or function
      constructors (`Function`, `GeneratorFunction`, etc) will throw an
      `EvalError`. **Default:** `true`.
    * `wasm` {boolean} If set to false any attempt to compile a WebAssembly
      module will throw a `WebAssembly.CompileError`. **Default:** `true`.

If given a `sandbox` object, the `vm.createContext()` method will [prepare
that sandbox][contextified] so that it can be used in calls to
[`vm.runInContext()`][] or [`script.runInContext()`][]. Inside such scripts,
the `sandbox` object will be the global object, retaining all of its existing
properties but also having the built-in objects and functions any standard
[global object][] has. Outside of scripts run by the vm module, global variables
will remain unchanged.

```js
const util = require('util');
const vm = require('vm');

global.globalVar = 3;

const sandbox = { globalVar: 1 };
vm.createContext(sandbox);

vm.runInContext('globalVar *= 2;', sandbox);

console.log(util.inspect(sandbox)); // { globalVar: 2 }

console.log(util.inspect(globalVar)); // 3
```

If `sandbox` is omitted (or passed explicitly as `undefined`), a new, empty
[contextified][] sandbox object will be returned.

The `vm.createContext()` method is primarily useful for creating a single
sandbox that can be used to run multiple scripts. For instance, if emulating a
web browser, the method can be used to create a single sandbox representing a
window's global object, then run all `<script>` tags together within the context
of that sandbox.

The provided `name` and `origin` of the context are made visible through the
Inspector API.

