<!-- YAML
added: v0.1.26
-->
- `eventName` {any}
- `listener` {Function}

从名为 `eventName` 的事件的监听器数组中移除指定的 `listener`。

```js
const callback = (stream) => {
  console.log('有连接！');
};
server.on('connection', callback);
// ...
server.removeListener('connection', callback);
```

`removeListener` 最多只会从监听器数组里移除一个监听器实例。
如果任何单一的监听器被多次添加到指定 `eventName` 的监听器数组中，则必须多次调用 `removeListener` 才能移除每个实例。

注意，一旦一个事件被触发，所有绑定到它的监听器都会按顺序依次触发。
这意味着，在事件触发后、最后一个监听器完成执行前，任何 `removeListener()` 或 `removeAllListeners()` 调用都不会从 `emit()` 中移除它们。
随后的事件会像预期的那样发生。

```js
const myEmitter = new MyEmitter();

const callbackA = () => {
  console.log('A');
  myEmitter.removeListener('event', callbackB);
};

const callbackB = () => {
  console.log('B');
};

myEmitter.on('event', callbackA);

myEmitter.on('event', callbackB);

// callbackA 移除了监听器 callbackB，但它依然会被调用。
// 触发是内部的监听器数组为 [callbackA, callbackB]
myEmitter.emit('event');
// 打印:
//   A
//   B

// callbackB 被移除了。
// 内部监听器数组为 [callbackA]
myEmitter.emit('event');
// 打印:
//   A

```

因为监听器是使用内部数组进行管理的，所以调用它会改变在监听器被移除后注册的任何监听器的位置索引。
虽然这不会影响监听器的调用顺序，但意味着由 `emitter.listeners()` 方法返回的监听器数组副本需要被重新创建。

返回一个 `EventEmitter` 引用，可以链式调用。

