
使用 `util.promisify.custom` 符号可以重写 [`util.promisify()`] 的返回值：

```js
const util = require('util');

function doSomething(foo, callback) {
  // ...
}

doSomething[util.promisify.custom] = (foo) => {
  return getPromiseSomehow();
};

const promisified = util.promisify(doSomething);
console.log(promisified === doSomething[util.promisify.custom]);
// 打印 'true'
```

对于原始函数不遵循将错误优先的回调作为最后一个参数的标准格式的情况，这很有用。

例如，使用一个接受 `(foo, onSuccessCallback, onErrorCallback)` 的函数:

```js
doSomething[util.promisify.custom] = (foo) => {
  return new Promise((resolve, reject) => {
    doSomething(foo, resolve, reject);
  });
};
```

如果定义了 `promisify.custom` 但不是一个函数，则 `promisify()` 将会抛出错误。

