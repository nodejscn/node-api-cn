
创建新的 `repl.REPLServer` 之后，提供用户自定义的解释功能。
举例来说，这可以用于实现完全用户自定义的 REPL 应用。

下列 REPL 例子实现了文字的翻译工作：

```js
const repl = require('repl');
const Translator = require('translator').Translator;

const myTranslator = new Translator('en', 'fr');

function myEval(cmd, context, filename, callback) {
  callback(null, myTranslator.translate(cmd));
}

repl.start({prompt: '> ', eval: myEval});
```

