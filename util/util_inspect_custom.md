<!-- YAML
added: v6.6.0
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/20857
    description: This is now defined as a shared symbol.
-->

* {symbol} that can be used to declare custom inspect functions.

In addition to being accessible through `util.inspect.custom`, this
symbol is [registered globally][global symbol registry] and can be
accessed in any environment as `Symbol.for('nodejs.util.inspect.custom')`.

```js
const inspect = Symbol.for('nodejs.util.inspect.custom');

class Password {
  constructor(value) {
    this.value = value;
  }

  toString() {
    return 'xxxxxxxx';
  }

  [inspect]() {
    return `Password <${this.toString()}>`;
  }
}

const password = new Password('r0sebud');
console.log(password);
// Prints Password <xxxxxxxx>
```

详见[自定义对象的查看函数][Custom inspection functions on Objects]。

