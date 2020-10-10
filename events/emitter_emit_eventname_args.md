<!-- YAML
added: v0.1.26
-->
* `eventName` {string|symbol}
- `...args` {any}
* 返回: {boolean}

按照监听器注册的顺序，同步地调用每个注册到名为 `eventName` 的事件的监听器，并传入提供的参数。

如果事件有监听器，则返回 `true`，否则返回 `false`。

```js
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

// 第一个监听器。
myEmitter.on('event', function firstListener() {
  console.log('第一个监听器');
});
// 第二个监听器。
myEmitter.on('event', function secondListener(arg1, arg2) {
  console.log(`第二个监听器中的事件有参数 ${arg1}、${arg2}`);
});
// 第三个监听器
myEmitter.on('event', function thirdListener(...args) {
  const parameters = args.join(', ');
  console.log(`第三个监听器中的事件有参数 ${parameters}`);
});

console.log(myEmitter.listeners('event'));

myEmitter.emit('event', 1, 2, 3, 4, 5);

// Prints:
// [
//   [Function: firstListener],
//   [Function: secondListener],
//   [Function: thirdListener]
// ]
// 第一个监听器
// 第二个监听器中的事件有参数 1、2
// 第三个监听器中的事件有参数 1, 2, 3, 4, 5
```

