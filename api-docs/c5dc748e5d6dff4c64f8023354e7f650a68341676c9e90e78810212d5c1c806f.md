<!-- YAML
added: v11.0.0
-->

<!-- type=global -->

* `callback` {Function} 要排队的函数。

`queueMicrotask()` 方法将微任务排队以调用 `callback`。 
如果 `callback` 抛出异常，则将会触发 [`process` 对象][`process` object] 的 `'uncaughtException'` 事件。

微任务队列由 V8 管理，可以与 [`process.nextTick()`] 队列（由 Node.js 管理）类似的方式使用。 
始终在 Node.js 事件循环的每个回合中的微任务队列之前处理 `process.nextTick()` 队列。

```js
// `queueMicrotask()` 用于确保 'load' 事件始终异步地触发，且因此保持一致。 
// 在这里使用 `process.nextTick()` 会导致 'load' 事件总是在任何其他 promise 任务之前触发。

DataHandler.prototype.load = async function load(key) {
  const hit = this._cache.get(url);
  if (hit !== undefined) {
    queueMicrotask(() => {
      this.emit('load', hit);
    });
    return;
  }

  const data = await fetchData(key);
  this._cache.set(url, data);
  this.emit('load', data);
};
```

