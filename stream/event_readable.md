<!-- YAML
added: v0.9.4
-->

`'readable'` 事件将在流中有数据可供读取时触发。在某些情况下，为 `'readable'` 事件添加回调将会导致一些数据被读取到内部缓存中。

```javascript
const readable = getReadableStreamSomehow();
readable.on('readable', () => {
  // 有一些数据可读了
});
```
当到达流数据尾部时， `'readable'` 事件也会触发。触发顺序在 `'end'` 事件之前。

事实上， `'readable'` 事件表明流有了新的动态：要么是有了新的数据，要么是到了流的尾部。 对于前者， [`stream.read()`][stream-read] 将返回可用的数据。而对于后者， [`stream.read()`][stream-read] 将返回
`null`。 例如，下面的例子中的 `foo.txt` 是一个空文件：

```js
const fs = require('fs');
const rr = fs.createReadStream('foo.txt');
rr.on('readable', () => {
  console.log('readable:', rr.read());
});
rr.on('end', () => {
  console.log('end');
});
```

上面交脚本的输出如下：

```txt
$ node test.js
readable: null
end
```

*注意*： 通常情况下，`readable.pipe()` 方法和 `'data'` 事件机制比 `'readable'` 事件更容易理解。
However, handling `'readable'` might result in increased throughput.

