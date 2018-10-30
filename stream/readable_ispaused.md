<!-- YAML
added: v0.11.14
-->

* 返回： {boolean}

返回可读流当前的操作状态。
主要用于 `readable.pipe()` 底层的机制。
大多数情况下无需直接使用该方法。

```js
const readable = new stream.Readable();

readable.isPaused(); // === false
readable.pause();
readable.isPaused(); // === true
readable.resume();
readable.isPaused(); // === false
```

