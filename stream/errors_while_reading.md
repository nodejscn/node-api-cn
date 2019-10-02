
在 [`readable._read()`] 执行期间发生的错误必须通过 [`readable.destroy(err)`][readable-_destroy] 方法冒泡。 
从 [`readable._read()`] 中抛出 `Error` 或手动触发 `'error'` 事件会导致未定义的行为。

```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    const err = checkSomeErrorCondition();
    if (err) {
      this.destroy(err);
    } else {
      // 做些处理。
    }
  }
});
```

