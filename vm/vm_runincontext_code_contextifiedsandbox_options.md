
* `code` {string} The JavaScript code to compile and run.
* `contextifiedSandbox` {Object} The [contextified][] object that will be used
  as the `global` when the `code` is compiled and run.
* `options`
  * `filename` {string} Specifies the filename used in stack traces produced
    by this script.
  * `lineOffset` {number} Specifies the line number offset that is displayed
    in stack traces produced by this script.
  * `columnOffset` {number} Specifies the column number offset that is displayed
    in stack traces produced by this script.
  * `displayErrors` {boolean} When `true`, if an [`Error`][] error occurs
    while compiling the `code`, the line of code causing the error is attached
    to the stack trace.
  * `timeout` {number} Specifies the number of milliseconds to execute `code`
    before terminating execution. If execution is terminated, an [`Error`][]
    will be thrown.

The `vm.runInContext()` method compiles `code`, runs it within the context of
the `contextifiedSandbox`, then returns the result. Running code does not have
access to the local scope. The `contextifiedSandbox` object *must* have been
previously [contextified][] using the [`vm.createContext()`][] method.

The following example compiles and executes different scripts using a single
[contextified][] object:

```js
const util = require('util');
const vm = require('vm');

const sandbox = { globalVar: 1 };
vm.createContext(sandbox);

for (let i = 0; i < 10; ++i) {
  vm.runInContext('globalVar *= 2;', sandbox);
}
console.log(util.inspect(sandbox));

// { globalVar: 1024 }
```

