<!-- YAML
added: v0.1.16
-->

* {Object}

`module.exports` 对象是由模块系统创建的。
有时这是难以接受的；许多人希望他们的模块成为某个类的实例。
为了实现这个，需要将期望导出的对象赋值给 `module.exports`。
注意，将期望的对象赋值给 `exports` 会简单地重新绑定本地 `exports` 变量，这可能不是期望的。

例子，假设创建了一个名为 `a.js` 的模块：

```js
const EventEmitter = require('events');

module.exports = new EventEmitter();

// 处理一些工作，并在一段时间后从模块自身触发 'ready' 事件。
setTimeout(() => {
  module.exports.emit('ready');
}, 1000);
```

然后，在另一个文件中可以这么做：

```js
const a = require('./a');
a.on('ready', () => {
  console.log('模块 a 已准备好');
});
```

注意，对 `module.exports` 的赋值必须立即完成。
不能在任何回调中完成。
以下是无效的：

x.js:

```js
setTimeout(() => {
  module.exports = { a: 'hello' };
}, 0);
```

y.js:

```js
const x = require('./x');
console.log(x.a);
```

