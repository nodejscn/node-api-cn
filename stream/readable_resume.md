<!-- YAML
added: v0.9.4
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18994
    description: The `resume()` has no effect if there is a `'readable'` event
                 listening.
-->

* 返回: {this}

将被暂停的可读流恢复触发 [`'data'`] 事件，并将流切换到流动模式。

`readable.resume()` 可以用来充分消耗流中的数据，但无需实际处理任何数据：

```js
getReadableStreamSomehow()
  .resume()
  .on('end', () => {
    console.log('到达流的尽头，但无需读取任何数据');
  });
```

当存在 `'readable'` 事件监听器时，`readable.resume()` 不起作用。
