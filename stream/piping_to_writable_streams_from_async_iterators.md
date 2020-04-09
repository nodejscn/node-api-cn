
在从异步迭代器写入可写流的场景中，应确保正确地处理背压和错误。

```js
const { once } = require('events');
const finished = util.promisify(stream.finished);

const writable = fs.createWriteStream('./file');

function drain(writable) {
  if (writable.destroyed) {
    return Promise.reject(new Error('过早关闭'));
  }
  return Promise.race([
    once(writable, 'drain'),
    once(writable, 'close')
      .then(() => Promise.reject(new Error('过早关闭')))
  ]);
}

async function pump(iterable, writable) {
  for await (const chunk of iterable) {
    // 处理 write() 上的背压。
    if (!writable.write(chunk)) {
      await drain(writable);
    }
  }
  writable.end();
}

(async function() {
  // 确保完成没有错误。
  await Promise.all([
    pump(iterable, writable),
    finished(writable)
  ]);
})();
```

在上面的示例中，`once()` 监听器会为 `'drain'` 事件捕获并抛出 `write()` 上的错误，因为 `once()` 也会处理 `'error'` 事件。
为了确保写入流的完成且没有错误，使用上面的 `finished()` 方法比使用 `'finish'` 事件的 `once()` 监听器更为安全。
在某些情况下，`'finish'` 之后可写流可能会触发 `'error'` 事件，并且 `once()` 将会在处理 `'finish'` 事件时释放 `'error'` 处理程序，这可能导致未处理的错误。

另外，可读流可以用 `Readable.from()` 封装，然后通过 `.pipe()` 传送：

```js
const finished = util.promisify(stream.finished);

const writable = fs.createWriteStream('./file');

(async function() {
  const readable = Readable.from(iterable);
  readable.pipe(writable);
  // 确保完成没有错误。
  await finished(writable);
})();
```

或者，使用 `stream.pipeline()` 传送流：

```js
const pipeline = util.promisify(stream.pipeline);

const writable = fs.createWriteStream('./file');

(async function() {
  const readable = Readable.from(iterable);
  await pipeline(readable, writable);
})();
```

<!--type=misc-->

