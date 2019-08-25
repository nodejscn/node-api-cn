<!-- YAML
added: v8.0.0
-->

* `original` {Function}
* 返回: {Function}

让一个遵循异常优先的回调风格的函数，即 `(err, value) => ...` 回调函数是最后一个参数，返回一个返回值是一个 promise 版本的函数。

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // 处理 `stats`。
}).catch((error) => {
  // 处理错误。
});
```

或者，使用 `async function` 获得等效的效果:

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);

async function callStat() {
  const stats = await stat('.');
  console.log(`该目录的所有者是 ${stats.uid}`);
}
```

如果原本就有 `original[util.promisify.custom]` 属性，`promisify` 会返回它的值，详见[自定义的 promise 化函数][Custom promisified functions]。

`promisify()` 会在所有情况下假定 `original` 是一个最后的参数是回调函数的函数。
如果 `original` 不是函数，则 `promisify()` 将会抛出错误。 
如果 `original` 是一个函数但它的最后一个参数不是错误优先回调，它仍然会传递一个错误优先回调作为它的最后一个参数。


