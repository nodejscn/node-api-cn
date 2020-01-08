<!-- YAML
added: v8.0.0
-->

* `original` {Function}
* 返回: {Function}

传入一个遵循常见的错误优先的回调风格的函数（即以 `(err, value) => ...` 回调作为最后一个参数），并返回一个返回 promise 的版本。

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // 使用 `stats`。
}).catch((error) => {
  // 处理错误。
});
```

或者，等效地使用 `async function`:

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);

async function callStat() {
  const stats = await stat('.');
  console.log(`该目录归 ${stats.uid} 拥有`);
}
```

如果存在 `original[util.promisify.custom]` 属性，则 `promisify` 将会返回其值，参阅[自定义的 promise 化函数][Custom promisified functions]。

`promisify()` 在所有情况下都会假定 `original` 是一个以回调作为其最后参数的函数。
如果 `original` 不是一个函数，则 `promisify()` 将会抛出错误。 
如果 `original` 是一个函数但其最后一个参数不是一个错误优先的回调，则它将仍会传入一个错误优先的回调作为其最后一个参数。

除非特殊处理，否则在类方法或使用 `this` 的其他方法上使用 `promisify()` 可能无法正常工作：

```js
const util = require('util');

class Foo {
  constructor() {
    this.a = 42;
  }

  bar(callback) {
    callback(null, this.a);
  }
}

const foo = new Foo();

const naiveBar = util.promisify(foo.bar);
// TypeError: Cannot read property 'a' of undefined
// naiveBar().then(a => console.log(a));

naiveBar.call(foo).then((a) => console.log(a)); // '42'

const bindBar = naiveBar.bind(foo);
bindBar().then((a) => console.log(a)); // '42'
```

