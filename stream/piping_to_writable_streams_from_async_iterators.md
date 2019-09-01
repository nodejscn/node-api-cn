
在从异步迭代器写入可写流的场景中，确保正确处理背压和错误非常重要。

```js
const { once } = require('events');

const writable = fs.createWriteStream('./file');

(async function() {
  for await (const chunk of iterator) {
    // 处理 write() 上的背压。
    if (!writable.write(chunk))
      await once(writable, 'drain');
  }
  writable.end();
  // 确保完成没有错误。
  await once(writable, 'finish');
})();
```

在以上示例中，两个 `once()` 监听器会捕获并抛出可写流上的错误，因 `once()` 也会处理 `'error'` 事件。

或者，可读流可以用 `Readable.from()` 封装，然后通过 `.pipe()` 传送：

```js
const { once } = require('events');

const writable = fs.createWriteStream('./file');

(async function() {
  const readable = Readable.from(iterator);
  readable.pipe(writable);
  // 确保完成没有错误。
  await once(writable, 'finish');
})();
```

<!--type=misc-->

