
建议在调用
`readable._read()` 方法时发生的错误应该执行触发 `'error'` 事件，而不是抛出异常错误。从`readable._read()`中抛出错误可能会导致意外的和不一致的行为，具体取决于流是以流还是暂停模式运行。 使用“错误”事件可确保一致且可预测的错误处理。

<!-- eslint-disable no-useless-return -->
```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    if (checkSomeErrorCondition()) {
      process.nextTick(() => this.emit('error', err));
      return;
    }
    // do some work
  }
});
```

