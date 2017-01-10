
The default evaluator provides access to any variables that exist in the global
scope. It is possible to expose a variable to the REPL explicitly by assigning
it to the `context` object associated with each `REPLServer`.  For example:

```js
const repl = require('repl');
var msg = 'message';

repl.start('> ').context.m = msg;
```

Properties in the `context` object appear as local within the REPL:

```js
$ node repl_test.js
> m
'message'
```

It is important to note that context properties are *not* read-only by default.
To specify read-only globals, context properties must be defined using
`Object.defineProperty()`:

```js
const repl = require('repl');
var msg = 'message';

const r = repl.start('> ');
Object.defineProperty(r.context, 'm', {
  configurable: false,
  enumerable: true,
  value: msg
});
```

