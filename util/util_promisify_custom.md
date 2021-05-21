<!-- YAML
added: v8.0.0
changes:
  - version:
      - v13.12.0
      - v12.16.2
    pr-url: https://github.com/nodejs/node/pull/31672
    description: 这现在被定义为一个共享的符号。
-->

* {symbol} 可被用于声明函数的自定义的 promise 化的变量，查看[自定义的 promise 化函数][Custom promisified functions]。

除了可以被通过 `util.promisify.custom` 访问之外，此符号被[全局地注册][global symbol registry]并且可以在任何环境中被作为 `Symbol.for('nodejs.util.promisify.custom')` 访问。

例如，使用一个接受 `(foo, onSuccessCallback, onErrorCallback)` 的函数：

```js
const kCustomPromisifiedSymbol = Symbol.for('nodejs.util.promisify.custom');

doSomething[kCustomPromisifiedSymbol] = (foo) => {
  return new Promise((resolve, reject) => {
    doSomething(foo, resolve, reject);
  });
};
```
