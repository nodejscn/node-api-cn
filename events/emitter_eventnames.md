<!-- YAML
added: v6.0.0
-->

返回一个列出触发器已注册监听器的事件的数组。
数组中的值为字符串或符号。 

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

