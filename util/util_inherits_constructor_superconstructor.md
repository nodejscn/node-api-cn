<!-- YAML
added: v0.3.0
changes:
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3455
    description: The `constructor` parameter can refer to an ES6 class now.
-->

注意，不建议使用 `util.inherits()`。
请使用 ES6 的 `class` 和 `extends` 关键词获得语言层面的继承支持。
注意，这两种方式是[语义上不兼容的]。

* `constructor` {Function}
* `superConstructor` {Function}

从一个[构造函数]中继承原型方法到另一个。
`constructor` 的原型会被设置到一个从 `superConstructor` 创建的新对象上。

`superConstructor` 可通过 `constructor.super_` 属性访问。

```js
const util = require('util');
const EventEmitter = require('events');

function MyStream() {
  EventEmitter.call(this);
}

util.inherits(MyStream, EventEmitter);

MyStream.prototype.write = function(data) {
  this.emit('data', data);
};

const stream = new MyStream();

console.log(stream instanceof EventEmitter); // true
console.log(MyStream.super_ === EventEmitter); // true

stream.on('data', (data) => {
  console.log(`接收的数据："${data}"`);
});
stream.write('运作良好！'); // 接收的数据："运作良好！"
```

例子：使用 ES6 的 `class` 和 `extends`：

```js
const EventEmitter = require('events');

class MyStream extends EventEmitter {
  write(data) {
    this.emit('data', data);
  }
}

const stream = new MyStream();

stream.on('data', (data) => {
  console.log(`接收的数据："${data}"`);
});
stream.write('使用 ES6');

```

