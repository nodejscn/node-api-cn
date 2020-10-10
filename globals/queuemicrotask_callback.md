<!-- YAML
added: v11.0.0
-->

<!-- type=global -->

* `callback` {Function} 要放入队列的函数。

`queueMicrotask()` 方法会将微任务放入队列以便调用 `callback`。 
如果 `callback` 抛出异常，则将会触发 [`process` 对象][`process` object]的 `'uncaughtException'` 事件。

微任务队列由 V8 进行管理，可以通过与 [`process.nextTick()`] 队列（由 Node.js 管理）类似的方式进行使用。 
在 Node.js 事件循环的每次轮询中，`process.nextTick()` 队列始终在微任务队列之前执行。

```js
// 在这里，`queueMicrotask()` 用于确保 'load' 事件总是异步地触发，且因此始终如一。 
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

