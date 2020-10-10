<!-- YAML
added: v8.0.0
changes:
  - version:
      - v13.12.0
      - v12.16.2
    pr-url: https://github.com/nodejs/node/pull/31672
    description: This is now defined as a shared symbol.
-->

* {symbol} 可用于声明函数的自定义的 promise 化变量，参见[自定义的 promise 化函数][Custom promisified functions]。

除了可以通过 `util.promisify.custom` 进行访问之外，该符号还被[注册为全局]的[global symbol registry]，并且可以在任何环境中作为 `Symbol.for('nodejs.util.promisify.custom')` 进行访问。

例如，使用一个接受 `(foo, onSuccessCallback, onErrorCallback)` 的函数：

```js
const kCustomPromisifiedSymbol = Symbol.for('nodejs.util.promisify.custom');

doSomething[kCustomPromisifiedSymbol] = (foo) => {
  return new Promise((resolve, reject) => {
    doSomething(foo, resolve, reject);
  });
};
```
