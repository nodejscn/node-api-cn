
When a new `repl.REPLServer` is created, a custom evaluation function may be
provided. This can be used, for instance, to implement fully customized REPL
applications.

创建新的`repl.REPLServer`之后，提供用户自定义的解读功能。举例来说，这可以用于实现完全用户自定义的REPL应用。

The following illustrates a hypothetical example of a REPL that performs
translation of text from one language to another:

下列REPL例子实现了文字的翻译工作

```js
const repl = require('repl');
const Translator = require('translator').Translator;

const myTranslator = new Translator('en', 'fr');

function myEval(cmd, context, filename, callback) {
  callback(null, myTranslator.translate(cmd));
}

repl.start({prompt: '> ', eval: myEval});
```

