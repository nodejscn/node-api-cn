<!-- YAML
added: v0.11.14
-->

* 返回： {boolean}

`readable.isPaused()` 方法返回可读流的当前操作状态。 该方法主要是在
`readable.pipe()` 方法的底层机制中用到。大多数情况下，没有必要直接使用该方法。

```js
const readable = new stream.Readable();

readable.isPaused(); // === false
readable.pause();
readable.isPaused(); // === true
readable.resume();
readable.isPaused(); // === false
```

