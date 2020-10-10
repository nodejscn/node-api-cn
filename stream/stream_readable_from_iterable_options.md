<!-- YAML
added:
  - v12.3.0
  - v10.17.0
-->

* `iterable` {Iterable} 实现 `Symbol.asyncIterator` 或 `Symbol.iterator` 可迭代协议的对象。Emits an 'error' event if a null
   value is passed.
* `options` {Object} 提供给 `new stream.Readable([options])` 的选项。 
   默认情况下，`Readable.from()` 会将 `options.objectMode` 设置为 `true`，除非通过将 `options.objectMode` 设置为 `false` 显式地选择此选项。
* 返回: {stream.Readable}

一个从迭代器中创建可读流的实用方法。

```js
const { Readable } = require('stream');

async function * generate() {
  yield 'hello';
  yield 'streams';
}

const readable = Readable.from(generate());

readable.on('data', (chunk) => {
  console.log(chunk);
});
```

出于性能原因，调用 `Readable.from(string)` 或 `Readable.from(buffer)` 将不会迭代字符串或 buffer 以匹配其他流的语义。

