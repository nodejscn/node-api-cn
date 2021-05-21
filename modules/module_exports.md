<!-- YAML
added: v0.1.16
-->

* {Object}

`module.exports` 对象是被 `Module` 系统创建的。
有时这是不可接受的；许多人希望他们的模块是某个类的一个实例。
为了这样做，则赋值期望的导出对象给 `module.exports`。
赋值期望的对象给 `exports` 会简单地重新绑定本地的 `exports` 变量，这可能不是所期望的。

例如，假设我们正在创建一个名为 `a.js` 的模块：

```js
const EventEmitter = require('events');

module.exports = new EventEmitter();

// 做一些工作，并且在一段时间之后从模块自身触发 'ready' 事件。
setTimeout(() => {
  module.exports.emit('ready');
}, 1000);
```

然后，在另一个文件中我们可以做：

```js
const a = require('./a');
a.on('ready', () => {
  console.log('模块 "a" 已就绪');
});
```

对 `module.exports` 的赋值必须被立即地完成。
它不能在任何回调中被完成。
这不会起作用：

`x.js`:

```js
setTimeout(() => {
  module.exports = { a: 'hello' };
}, 0);
```

`y.js`:

```js
const x = require('./x');
console.log(x.a);
```

