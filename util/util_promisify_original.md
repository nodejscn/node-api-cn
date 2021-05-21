<!-- YAML
added: v8.0.0
-->

* `original` {Function}
* 返回: {Function}

传入一个遵循常见的错误优先的回调风格的函数（即以一个 `(err, value) => ...` 回调作为最后一个参数），并且返回一个返回 promise 的版本。

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // 使用 `stats` 做些事情
}).catch((error) => {
  // 处理错误。
});
```

或者，等效地使用 `async function`：

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);

async function callStat() {
  const stats = await stat('.');
  console.log(`此目录被 ${stats.uid} 拥有`);
}
```

如果存在一个 `original[util.promisify.custom]` 属性，则 `promisify` 会返回其值，查看[自定义的 promise 化函数][Custom promisified functions]。

`promisify()` 假定在所有情况下 `original` 都是一个以一个回调作为其最后一个参数的函数。
如果 `original` 不是一个函数，则 `promisify()` 会抛出一个错误。 
如果 `original` 是一个函数但是其最后一个参数不是一个错误优先的回调，则它仍然会被传入一个错误优先的回调作为其最后一个参数。

在类方法或使用 `this` 的其他方法上使用 `promisify()` 可能无法正常工作，除非被特殊地处理：

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

