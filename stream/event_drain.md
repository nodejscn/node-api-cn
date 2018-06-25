<!-- YAML
added: v0.9.4
-->

如果调用 [`stream.write(chunk)`][stream-write] 方法返回 `false`，则在适合恢复写入数据到流时触发 `'drain'` 事件。

```js
// 向提供的可写流中写入数据一百万次。
// 注意背压（back-pressure）。
function writeOneMillionTimes(writer, data, encoding, callback) {
  let i = 1000000;
  write();
  function write() {
    let ok = true;
    do {
      i--;
      if (i === 0) {
        // 最后一次。
        writer.write(data, encoding, callback);
      } else {
        // 检查是否可以继续写入。 
        // 不要传入 callback，因为写入还没有结束。
        ok = writer.write(data, encoding);
      }
    } while (i > 0 && ok);
    if (i > 0) {
      // 不得不提前停下！
      // 当 'drain' 事件触发后继续写入。
      writer.once('drain', write);
    }
  }
}
```

