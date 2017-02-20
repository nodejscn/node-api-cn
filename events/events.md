
> 稳定性: 2 - 稳定的

<!--type=module-->

大多数 Node.js 核心 API 都是采用惯用的异步事件驱动架构，其中某些类型的对象（称为触发器）会周期性地触发命名事件来调用函数对象（监听器）。

例如，一个 [`net.Server`] 对象会在每次有新连接时触发一个事件；一个 [`fs.ReadStream`] 会在文件被打开时触发一个事件；一个 [stream] 会在数据可读时触发事件。

所有能触发事件的对象都是 `EventEmitter` 类的实例。
这些对象开放了一个 `eventEmitter.on()` 函数，允许将一个或多个函数附加到会被对象触发的命名事件上。
事件名称通常是驼峰式的字符串，但也可以使用任何有效的 JavaScript 属性名。

当 `EventEmitter` 对象触发一个事件是，所有附加在特定事件上的函数都被同步地调用。
被调用的监听器返回的值都会被忽略并丢弃。

以下例子展示了一个只有单个监听器的 `EventEmitter` 实例。
`eventEmitter.on()` 方法用于注册监听器，`eventEmitter.emit()` 方法用于触发事件。


```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('发生了一个事件！');
});
myEmitter.emit('event');
```

