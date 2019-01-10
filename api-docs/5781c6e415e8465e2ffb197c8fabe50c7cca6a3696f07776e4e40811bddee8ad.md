<!-- YAML
added: v0.1.26
-->
* `eventName` {string|symbol} 事件名称。
* `listener` {Function} 监听器。
* 返回: {EventEmitter}


从名为 `eventName` 的事件的监听器数组中移除指定的 `listener`。

```js
const callback = (stream) => {
  console.log('已连接');
};
server.on('connection', callback);
// ...
server.removeListener('connection', callback);
```

`removeListener()` 最多只会从监听器数组中移除一个监听器。
如果监听器被多次添加到指定 `eventName` 的监听器数组中，则必须多次调用 `removeListener()` 才能移除所有实例。

一旦事件被触发，所有绑定到该事件的监听器都会按顺序依次调用。
这意味着，在事件触发之后、且最后一个监听器执行完成之前，`removeListener()` 或 `removeAllListeners()` 不会从 `emit()` 中移除它们。

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
// 触发时内部的监听器数组为 [callbackA, callbackB]
myEmitter.emit('event');
// 打印:
//   A
//   B

// callbackB 现已被移除。
// 内部的监听器数组为 [callbackA]
myEmitter.emit('event');
// 打印:
//   A

```

