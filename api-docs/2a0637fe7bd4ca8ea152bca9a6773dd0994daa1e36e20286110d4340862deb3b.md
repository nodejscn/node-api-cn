<!-- YAML
added: v0.9.4
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17979
    description: >
      The `'readable'` is always emitted in the next tick after `.push()`
      is called
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18994
    description: Using `'readable'` requires calling `.read()`.
-->

当流中有数据可供读取时触发。

```javascript
const readable = getReadableStreamSomehow();
readable.on('readable', function() {
  // 有数据可读取。
  let data;

  while (data = this.read()) {
    console.log(data);
  }
});
```

当到达流数据的尽头时，`'readable'` 事件也会触发，但是在 `'end'` 事件之前触发。

`'readable'` 事件表明流有新的动态：要么有新的数据，要么到达流的尽头。
对于前者，[`stream.read()`][stream-read] 会返回可用的数据。
对于后者，[`stream.read()`][stream-read] 会返回 `null`。
例如，下面的例子中，`foo.txt` 是一个空文件：

```js
const fs = require('fs');
const rr = fs.createReadStream('foo.txt');
rr.on('readable', () => {
  console.log(`读取的数据: ${rr.read()}`);
});
rr.on('end', () => {
  console.log('结束');
});
```

运行上面的脚本输出如下：

```txt
$ node test.js
读取的数据: null
结束
```

通常情况下，`readable.pipe()` 和 `'data'` 事件的机制比 `'readable'` 事件更容易理解。
处理 `'readable'` 事件可能造成吞吐量升高。

如果同时使用 `'readable'` 事件和 [`'data'`] 事件，则 `'readable'` 事件会优先控制流，也就是说，当调用 [`stream.read()`][stream-read] 时才会触发 `'data'` 事件。
`readableFlowing` 属性会变成 `false`。
当移除 `'readable'` 事件时，如果存在 `'data'` 事件监听器，则流会开始流动，也就是说，无需调用 `.resume()` 也会触发 `'data'` 事件。

