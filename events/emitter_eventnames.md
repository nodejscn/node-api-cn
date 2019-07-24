<!-- YAML
added: v6.0.0
-->

* 返回: {Array}

返回已注册监听器的事件名数组。
数组中的值为字符串或 `Symbol`。

```js
const EventEmitter = require('events');
const myEE = new EventEmitter();
myEE.on('foo', () => {});
myEE.on('bar', () => {});

const sym = Symbol('symbol');
myEE.on(sym, () => {});

console.log(myEE.eventNames());
// 打印: [ 'foo', 'bar', Symbol(symbol) ]
```

