<!-- YAML
added: v0.3.1
-->

* `code` {string} The JavaScript code to compile and run.
* `sandbox` {Object} An object that will be [contextified][]. If `undefined`, a
  new object will be created.
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

The `vm.runInNewContext()` first contextifies the given `sandbox` object (or
creates a new `sandbox` if passed as `undefined`), compiles the `code`, runs it
within the context of the created context, then returns the result. Running code
does not have access to the local scope.

The following example compiles and executes code that increments a global
variable and sets a new one. These globals are contained in the `sandbox`.

```js
const util = require('util');
const vm = require('vm');

const sandbox = {
  animal: 'cat',
  count: 2
};

vm.runInNewContext('count += 1; name = "kitty"', sandbox);
console.log(util.inspect(sandbox));

// { animal: 'cat', count: 3, name: 'kitty' }
```

