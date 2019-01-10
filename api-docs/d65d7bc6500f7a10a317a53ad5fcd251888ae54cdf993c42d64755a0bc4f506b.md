
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

<!--type=module-->

大多数 Node.js 核心 API 构建于惯用的异步事件驱动架构，其中某些类型的对象（又称触发器，Emitter）会触发命名事件来调用函数（又称监听器，Listener）。

例如，[`net.Server`] 会在每次有新连接时触发事件，[`fs.ReadStream`] 会在打开文件时触发事件，[stream]会在数据可读时触发事件。

所有能触发事件的对象都是 `EventEmitter` 类的实例。
这些对象有一个 `eventEmitter.on()` 函数，用于将一个或多个函数绑定到命名事件上。
事件的命名通常是驼峰式的字符串。

当 `EventEmitter` 对象触发一个事件时，所有绑定在该事件上的函数都会被同步地调用。

例子，一个简单的 `EventEmitter` 实例，绑定了一个监听器。
`eventEmitter.on()` 用于注册监听器，`eventEmitter.emit()` 用于触发事件。

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('触发事件');
});
myEmitter.emit('event');
```

