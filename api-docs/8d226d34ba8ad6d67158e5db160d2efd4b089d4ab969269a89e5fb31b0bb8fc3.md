
当 `readable._read()` 在执行期间发生的错误时，建议触发 `'error'` 事件而不是抛出错误。
从 `readable._read()` 中抛出错误可能会导致无法预期的结果。
使用`'error'` 事件可以确保对错误进行一致且可预测的处理。

<!-- eslint-disable no-useless-return -->
```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    if (checkSomeErrorCondition()) {
      process.nextTick(() => this.emit('error', err));
      return;
    }
    // 各种处理。
  }
});
```

