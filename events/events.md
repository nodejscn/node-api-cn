
> 稳定性: 2 - 稳定的

<!--type=module-->

大多数 Node.js 核心 API 都采用惯用的异步事件驱动架构，其中某些类型的对象（触发器）会周期性地触发命名事件来调用函数对象（监听器）。

例如，[`net.Server`] 对象会在每次有新连接时触发事件；[`fs.ReadStream`] 会在文件被打开时触发事件；[流对象] 会在数据可读时触发事件。

所有能触发事件的对象都是 `EventEmitter` 类的实例。
这些对象开放了一个 `eventEmitter.on()` 函数，允许将一个或多个函数绑定到会被对象触发的命名事件上。
事件名称通常是驼峰式的字符串，但也可以使用任何有效的 JavaScript 属性名。

当 `EventEmitter` 对象触发一个事件时，所有绑定在该事件上的函数都被同步地调用。
监听器的返回值会被丢弃。

例子，一个绑定了一个监听器的 `EventEmitter` 实例。
`eventEmitter.on()` 方法用于注册监听器，`eventEmitter.emit()` 方法用于触发事件。

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('触发了一个事件！');
});
myEmitter.emit('event');
```

