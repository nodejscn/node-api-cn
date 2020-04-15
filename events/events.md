
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

<!--type=module-->

大多Node.js 核心API都围绕一种异步事件驱动架构而建。此架构中，特定的一类叫做发射器("emitters")的对象通过触发具名事件使函数对象（所谓"监听器"）被调用。

例如，每当有对等连接时，一个[`net.Server`] 对象会在触发事件；每当文件打开时，一个[`fs.ReadStream`] 对象会触发事件；每当数据可读时，一个[stream]对象会在触发事件。

所有能触发事件的对象都是 `EventEmitter` 类的实例。
这些对象有一个 `eventEmitter.on()` 函数，用于将一个或多个函数绑定到具名事件上。
事件的名称通常是驼峰式的字符串，但也可以使用任何有效的 JavaScript 属性键。。

当 `EventEmitter` 对象触发一个事件时，所有绑定在该事件上的函数都会被同步地调用。
被调用的监听器返回的任何值都将会被忽略并丢弃。

如下，一个简单的 `EventEmitter` 实例，绑定了一个监听器。
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

