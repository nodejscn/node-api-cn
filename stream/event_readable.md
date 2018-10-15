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
当到达流数据尾部时， `'readable'` 事件也会触发。触发顺序在 `'end'` 事件之前。

事实上， `'readable'` 事件表明流有了新的动态：要么是有了新的数据，要么是到了流的尾部。 对于前者， [`stream.read()`][stream-read] 将返回可用的数据。而对于后者， [`stream.read()`][stream-read] 将返回
`null`。 例如，下面的例子中的 `foo.txt` 是一个空文件：

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

*注意*： 通常情况下，`readable.pipe()` 方法和 `'data'` 事件机制比 `'readable'` 事件更容易理解。然而处理 `'readable'`事件可能造成吞吐量升高。


