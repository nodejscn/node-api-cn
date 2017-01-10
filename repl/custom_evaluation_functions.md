
When a new `repl.REPLServer` is created, a custom evaluation function may be
provided. This can be used, for instance, to implement fully customized REPL
applications.

The following illustrates a hypothetical example of a REPL that performs
translation of text from one language to another:

```js
const repl = require('repl');
const Translator = require('translator').Translator;

const myTranslator = new Translator('en', 'fr');

function myEval(cmd, context, filename, callback) {
  callback(null, myTranslator.translate(cmd));
}

repl.start({prompt: '> ', eval: myEval});
```

