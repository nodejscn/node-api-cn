<!-- YAML
added: v0.11.0
-->

The `'reset'` event is emitted when the REPL's context is reset. This occurs
whenever the `.clear` command is received as input *unless* the REPL is using
the default evaluator and the `repl.REPLServer` instance was created with the
`useGlobal` option set to `true`. The listener callback will be called with a
reference to the `context` object as the only argument.

This can be used primarily to re-initialize REPL context to some pre-defined
state as illustrated in the following simple example:

```js
const repl = require('repl');

function initializeContext(context) {
  context.m = 'test';
}

var r = repl.start({prompt: '>'});
initializeContext(r.context);

r.on('reset', initializeContext);
```

When this code is executed, the global `'m'` variable can be modified but then
reset to its initial value using the `.clear` command:

```js
$ ./node example.js
>m
'test'
>m = 1
1
>m
1
>.clear
Clearing context...
>m
'test'
>
```

