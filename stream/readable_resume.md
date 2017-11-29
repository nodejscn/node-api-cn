<!-- YAML
added: v0.9.4
-->

* 返回： `this`

`readable.resume()` 方法会重新触发 [`'data'`][] 事件, 将暂停模式切换到流动模式。

`readable.resume()` 方法可以用来充分使用流中的数据，而不用实际处理任何数据，如以下示例所示：

```js
getReadableStreamSomehow()
  .resume()
  .on('end', () => {
    console.log('Reached the end, but did not read anything.');
  });
```

