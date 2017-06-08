<!-- YAML
added: v8.0.0
-->

* `original` {Function}

让一个遵循通常的 Node.js 回调风格的函数， 即 `(err, value) => ...` 回调函数是最后一个参数, 返回一个返回值是一个 promise 版本的函数。

例如：

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // Do something with `stats`
}).catch((error) => {
  // Handle the error.
});
```

或者，使用`async function`获得等效的效果:

```js
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);

async function callStat() {
  const stats = await stat('.');
  console.log(`This directory is owned by ${stats.uid}`);
}
```

如果原本就有 `original[util.promisify.custom]` 属性, `promisify` 会返回它的值， 查阅 [Custom promisified functions][].

`promisify()` 会在所有情况下假定 `original` 是一个最后的参数是回调函数的函数，如果它不是，那么返回的函数的返回值为 undefined。 

